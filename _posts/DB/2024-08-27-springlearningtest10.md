---
layout: single
title: "[Spring-HTTP-CLIENT-1] RestTemplate, RestClient"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Spring의 HTTP 클라이언트

스프링 프레임워크는 다양한 HTTP 클라이언트를 제공하여 애플리케이션이 외부 API와 통신할 수 있도록 합니다.        
스프링이 제공하는 HTTP 클라이언트에는 `RestClient`, `WebClient`, `RestTemplate` 이 있습니다.        

이 문서에서는 `RestTemplate`과 스프링 6.1 버전에 추가된 `RestClient` 에 대해 다룹니다.

HTTP Client : 애플리케이션이 외부 API와의 통신을 도움.

- RestClient
- WebClient
- RestTemplate

---

# 2. RestTemplate

## 2-1. GET 요청 하기

`RestTemplate` 의 `getForEntity()` 메서드를 사용해 GET 요청을 하고 응답을 원하는 **POJO**로 변환할 수 있습니다.

> **POJO** : **객체 지향적인 원리**에 충실하면서 **환경과 기술에 종속되지 않고**, 필요에 따라 **재활용**될 수 있는 방식으로 설계된 오브젝트.
> 
> 
> 간단하게 말해서 **필드와 Getter, Setter와 같은 기본 기능만**을 갖는 기본 객체를 의미한다.
> 
> 자세히는 특정 **"기술"에 종속되 있는 상태로 개발하지 않는 개념**을 위해 등장한 언어이다.
> 
> 출처: [https://ittrue.tistory.com/211](https://ittrue.tistory.com/211) [IT is True:티스토리]
> 
> [https://wooj-coding-fordeveloper.tistory.com/80#아마 자바 스프링 개발자이기에 해당 내용이 궁금할 것이다.-1](https://wooj-coding-fordeveloper.tistory.com/80#%EC%95%84%EB%A7%88%20%EC%9E%90%EB%B0%94%20%EC%8A%A4%ED%94%84%EB%A7%81%20%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%9D%B4%EA%B8%B0%EC%97%90%20%ED%95%B4%EB%8B%B9%20%EB%82%B4%EC%9A%A9%EC%9D%B4%20%EA%B6%81%EA%B8%88%ED%95%A0%20%EA%B2%83%EC%9D%B4%EB%8B%A4.-1)
> 

- restTemplate을 사용하여 요청을 보내고 결과를 Todo로 변환하여 반환
    
    ```java
    restTemplate.getForEntity( 
    		String url,
        Class<T> responseType,
        Object... uriVariables (option)
    )
    ```
    

### 참고자료

- [The Guide to RestTemplate](https://www.baeldung.com/rest-template)

## 2-2. 예외 처리

`RestTemplate` 을 사용해 외부 API와 통신할 때, 응답 코드에 따라 예외처리를 할 수 있습니다.

- 존재하지 않는 id로 요청을 보낼 경우 TodoException.NotFound 예외를 던짐
    - `*NOT_FOUND`* ⇒ `HttpStatus.*NOT_FOUND`* ⇒ `e.getStatusCode()` ⇒ `HttpClientErrorException e`
    

### 참고자료

- [Spring RestTemplate Error Handling](https://www.baeldung.com/spring-rest-template-error-handling)

---

# 3. RestClient

## 3-1. GET 요청 하기

`RestClient` 의 `get()` 메서드를 사용해 GET 요청을 할 수 있습니다.

- 외부 API의 host는 `RestClientConfig` 에 설정한다.
    - `RestClient.*builder*().baseUrl("http://jsonplaceholder.typicode.com").build()`
    - ⇒ `uri("/todos")`

```java
String result = restClient.get() 
  .uri("https://example.com") 
  .retrieve() 
  .body(String.class);
```

### 참고자료

- [Spring - REST Clients](https://docs.spring.io/spring-framework/reference/integration/rest-clients.html)
- [Spring blog - New in Spring 6.1: RestClient](https://spring.io/blog/2023/07/13/new-in-spring-6-1-restclient)

## 3-2. GET 요청의 응답 변환하기

`RestClient` 의 `body()` 메서드를 사용해 응답을 원하는 POJO로 변환할 수 있습니다.

- restClient의 get메서드를 사용하여 요청을 보내고 결과를 Todo로 변환하여 반환

```java
Todo todo = restClient.get()
  .uri("/todos/{id}", id)
  .retrieve()
  .body(Todo.class);
```

## 3-3. 예외 처리

`RestClient` 의 `onStatus()` 메서드를 사용해 HTTP 응답 코드에 따라 예외처리를 할 수 있습니다.

- 존재하지 않는 id로 요청을 보낼 경우 TodoException.NotFound 예외를 던짐
    - 특정 Status code에 대한 예외처리
        
        ```java
        .onStatus(status -> status.value() == 404, (req, res) -> {
              throw new TodoException.NotFound(id);
          })
        ```
        
    - 400번대 통들어 예외 처리
        
        ```java
        .onStatus(HttpStatusCode::is4xxClientError, (request, response) -> { 
              throw new TodoException.NotFound(id);
          })
        ```
        

- onStatus()

```java
onStatus(
   Predicate<HttpStatus> statusPredicate,
   BiFunction<ClientRequest, ClientResponse, Mono<? extends Throwable>> exceptionFunction
)
```

- **statusPredicate**: `status -> status.value() == 404`
    
    `HttpStatus`를 입력받아 `true` 또는 `false`를 반환
    
- **exceptionFunction:** `(req, res) -> { throw new TodoException.NotFound(id);}`
    
    해당 상태 코드에 대응하는 예외를 생성하는 람다 함수
    

---

# 4. 더 생각해보기

## `POST`, `PUT`, `DELETE` 등 다른 HTTP 메서드

- [https://jsonplaceholder.typicode.com/guide/](https://jsonplaceholder.typicode.com/guide/) 를 참고해 다른 메서드에 대한 API를 사용합니다.

### RestTemplate

- `POST` (Create)
    - `restTemplate.postForEntity(resourceUrl, newTodo, Todo.class)`
    
    ```java
    restTemplate.postForEntity(     
    		String url,
        @Nullable Object request,
        Class<T> responseType,
        Object... uriVariables 
    )
    ```
    
- `PUT` (Update)
    - `restTemplate.exchange(resourceUrl, HttpMethod.*PUT*, requestUpdate, Todo.class, id)`
    
    ```java
    restTemplate.exchange(     
    		String url,
        org.springframework.http.HttpMethod method,
        @Nullable org.springframework.http.HttpEntity<?> requestEntity,
        Class<T> responseType,
        Object... uriVariables 
    )
    ```
    
- `DELETE` (Delete)
    - `restTemplate.delete(resourceUrl, id)`
    
    ```java
    restTemplate.delete(     
    		String url,
        Object... uriVariables 
    )
    ```
    
    - JSONPlaceholder API는 실제로 데이터를 삭제하지 않습니다. 이는 모의 API이므로 `DELETE` 요청을 보내도 실제 데이터는 삭제되지 않습니다.
    - JSONPlaceholder는 모의(mock) API이며, 실제로 데이터를 삭제하지 않고 성공적인 삭제 작업을 시뮬레이션합니다. 이 과정에서 200 OK를 반환하도록 설계되었습니다.

### RestClient

- `POST` (Create)
    
    ```java
    restClient.post()
            .uri("/todos")
            .body(newTodo)
            .retrieve()
            .body(Todo.class); 
    ```
    
- `PUT` (Update)
    
    ```java
    restClient.put()
            .uri("/todos/{id}", id)
            .body(updatedTodo)
            .retrieve()
            .body(Todo.class); 
    ```
    
- `DELETE` (Delete)
    
    ```java
    restClient.delete()
            .uri("/todos/{id}", id)
            .retrieve()
            .toBodilessEntity();
    ```
    
- `toBodilessEntity()` : DELETE 요청에 대한 응답 본문이 필요 없으므로 toBodilessEntity 사용

## RestTemplate, RestClient, WebClient 특징과 차이점

### 1. `RestTemplate`

특징:

- **오래된 기술**: Spring 3.0부터 도입된 클래식한 HTTP 클라이언트입니다.
- **블로킹 I/O**: `RestTemplate`은 동기 방식으로 동작하며, 호출된 HTTP 요청은 서버로부터 응답이 올 때까지 스레드를 차단(blocking)합니다.
- **간단한 API**: 매우 간단한 API를 제공하여 학습 곡선이 낮습니다. 주로 단순한 HTTP 요청/응답을 처리할 때 사용됩니다.
- **Deprecated 예정**: Spring 5.0 이후로는 더 이상 권장되지 않으며, 비동기 및 리액티브 프로그래밍을 지원하는 `WebClient`로 대체되고 있습니다.

사용 예시:

- **간단한 동기 HTTP 요청이 필요한 경우**: 외부 API 호출이 간단하고, 동기적으로 결과를 받아 처리하는 경우에 사용합니다.
- **레거시 코드 유지**: 기존에 `RestTemplate`을 사용 중인 애플리케이션에서 코드를 유지 보수할 때 사용합니다.

### 2. `RestClient`

특징:

- **Spring Boot 3.1부터 도입**: `RestTemplate`과 `WebClient`의 간단함을 결합한 새로운 HTTP 클라이언트입니다.
- **동기 및 비동기 모두 지원**: 기존의 `RestTemplate`처럼 간단하지만, 비동기 처리 또한 지원하여 좀 더 유연하게 사용할 수 있습니다.
- **더 나은 API 디자인**: `RestClient`는 쉽게 설정하고 사용 가능한 API를 제공합니다.
- **대체 수단**: `RestTemplate`과 `WebClient`의 장점을 통합하여 향후 Spring에서 널리 사용될 가능성이 큽니다.

사용 예시:

- **새로운 프로젝트**: 새로운 Spring 프로젝트를 시작할 때 `RestClient`를 고려할 수 있습니다.
- **동기 및 비동기 HTTP 요청**: 둘 다 쉽게 처리하고자 할 때 유용합니다.

### 3. `WebClient`

특징:

- **Spring 5.0 이상에서 도입**: `RestTemplate`의 대체 기술로 리액티브 프로그래밍 모델을 지원합니다.
- **비동기 및 논블로킹 I/O**: HTTP 요청이 비동기적으로 처리되며, 결과를 받기 전까지 스레드가 차단되지 않습니다. 이를 통해 더 높은 성능과 확장성을 제공합니다.
- **리액티브 스트림**: Project Reactor를 기반으로 하여, 리액티브 스트림을 사용하여 비동기 처리를 더욱 쉽게 구현할 수 있습니다.
- **유연성**: 요청과 응답의 커스터마이징이 용이하며, `ExchangeFilterFunction`을 사용해 필터링을 추가할 수 있습니다.

사용 예시:

- **리액티브 시스템**: 비동기 처리와 높은 성능이 요구되는 리액티브 애플리케이션에서 사용됩니다.
- **대규모 트래픽 처리**: 스케일링이 필요한 서비스에서 `WebClient`의 비동기 및 논블로킹 I/O가 큰 이점을 제공합니다.

## 외부 API와 통신할 때 발생할 수 있는 예외 상황

### 1. **네트워크 연결 오류 (Connection Timeout, ConnectException)**

- **설명**: 외부 API 서버에 연결하는 동안 네트워크 문제로 인해 **연결이 실패**하거나 **시간 초과**가 발생할 수 있습니다.
- **처리 방안**:
    - **재시도 로직 구현**: 일정한 지연 시간을 두고 재시도하도록 합니다. 이때, 지수 백오프(exponential backoff) 전략을 사용하면 네트워크 부하를 줄일 수 있습니다.
    - **백업 API 사용**: 가능한 경우 다른 백업 API 엔드포인트로 요청을 시도할 수 있습니다.
    - **적절한 예외 처리 및 사용자 알림**: 사용자에게 네트워크 문제로 인해 요청이 실패했음을 알리고, 문제가 해결될 때까지 기다리도록 안내합니다.

### 2. **HTTP 상태 코드 오류 (4xx, 5xx 에러)**

- **설명**: 4xx 에러는 **클라이언트 측 오류**(예: 400 Bad Request, 401 Unauthorized, 403 Forbidden 등), 5xx 에러는 **서버 측 오류**(예: 500 Internal Server Error, 503 Service Unavailable 등)를 나타냅니다.
- **처리 방안**:
    - **4xx 에러 처리**: 클라이언트 측 요청에 문제가 있을 수 있으므로, 요청을 다시 확인하고 수정합니다. 특히 401이나 403과 같은 권한 관련 에러는 인증 정보를 재검토하거나 사용자에게 재인증을 요청해야 합니다.
    - **5xx 에러 처리**: 서버 측 문제로 인한 것이므로, 재시도 로직을 통해 일정 시간 후에 다시 요청하거나 사용자에게 서버가 일시적으로 사용 불가 상태임을 알립니다.
    - **로깅 및 모니터링**: 에러 상황을 로깅하여 문제가 자주 발생하는지 모니터링하고, 필요 시 관리자에게 알림을 보낼 수 있습니다.

### 3. **데이터 포맷 오류 (JsonParseException, JsonMappingException)**

- **설명**: API 응답 데이터가 예상한 형식이 아니거나 **JSON 형식이 깨진 경우** 발생할 수 있습니다.
- **처리 방안**:
    - **응답 데이터 검증**: 응답 데이터의 유효성을 검증하여, 예상된 형식이 아닌 경우 적절한 예외를 발생시키고 처리합니다.
    - **에러 핸들러**: JSON 파싱 오류가 발생할 경우 사용자에게 데이터를 처리할 수 없음을 알리고, 서버에 문제를 보고하거나 관리자에게 알림을 보냅니다.
    - **로깅**: 문제가 발생한 응답 데이터를 로깅하여 추후 분석할 수 있도록 합니다.

### 4. **응답 지연 (Read Timeout, Slow Response)**

- **설명**: API 서버가 응답을 반환하는 데 예상보다 **오래 걸리는 경우**입니다.
- **처리 방안**:
    - **타임아웃 설정**: 적절한 타임아웃 값을 설정하여 너무 오래 기다리지 않도록 합니다. 타임아웃이 발생하면 요청을 취소하고 사용자에게 알립니다.
    - **로딩 상태 제공**: 사용자에게 로딩 중임을 알리는 UI를 제공하여 응답이 지연되고 있음을 시각적으로 표시합니다.
    - **백그라운드 처리**: 응답이 느린 작업을 비동기적으로 처리하여 UI가 응답성을 유지하도록 합니다.

### 5. **권한 부족 (Unauthorized, Forbidden)**

- **설명**: 인증이나 권한이 부족하여 API 요청이 거부될 수 있습니다.
- **처리 방안**:
    - **재인증 요청**: 만료된 인증 토큰이 원인일 수 있으므로, 사용자에게 다시 로그인하도록 유도합니다.
    - **적절한 메시지 표시**: 사용자에게 권한 부족을 설명하고, 필요한 권한을 얻을 수 있는 방법을 안내합니다.
    - **로깅**: 불법적인 접근 시도가 있을 경우 이를 로깅하고, 보안 관련 알림을 트리거합니다.

### 6. **서비스 불가 (Service Unavailable, Circuit Breaker Open)**

- **설명**: API 서비스가 **일시적으로 사용 불가 상태**이거나 **서킷 브레이커**가 열려 요청이 차단된 경우입니다.
- **처리 방안**:
    - **재시도 로직**: 일정 시간이 지난 후 재시도를 하거나, 다른 대체 경로로 요청을 시도합니다.
    - **서킷 브레이커 패턴**: 서킷 브레이커 패턴을 적용하여 서비스가 복구될 때까지 일정 시간 동안 요청을 차단하고 대체 동작을 수행합니다.
    - **적절한 알림**: 사용자에게 서비스가 일시적으로 사용 불가 상태임을 알리고, 대체 행동을 안내합니다.

### 7. **잘못된 응답 (Unexpected Response Data)**

- **설명**: API가 예상하지 못한 데이터를 반환하는 경우입니다.
- **처리 방안**:
    - **데이터 검증**: 응답 데이터의 형식과 값을 검증하여 예상치 못한 데이터가 반환된 경우 이를 처리하는 로직을 추가합니다.
    - **로깅**: 예상치 못한 응답 데이터를 로깅하고, 필요 시 해당 문제를 분석합니다.
    - **fallback 처리**: 예상치 못한 데이터를 처리할 수 있는 기본 값이나 대체 동작을 제공하여 애플리케이션이 중단되지 않도록 합니다.

### 8. **API 요청 제한 초과 (Rate Limiting)**

- **설명**: 일정 시간 내에 **너무 많은 요청**을 보내서 **API의 요청 제한을 초과**하는 경우입니다.
- **처리 방안**:
    - **지수 백오프 전략**: 요청 제한 초과 시 요청을 지연시키고, 일정 시간 후에 다시 시도하는 전략을 적용합니다.
    - **캐싱**: 동일한 데이터를 여러 번 요청할 필요가 없는 경우 응답을 캐싱하여 API 요청 수를 줄입니다.
    - **적절한 메시지 전달**: 사용자에게 요청이 제한되었음을 알리고, 잠시 후에 다시 시도할 것을 안내합니다.
