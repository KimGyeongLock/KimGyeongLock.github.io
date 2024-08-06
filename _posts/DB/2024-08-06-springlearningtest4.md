---
layout: single
title: "[Spring-MVC-4] MVC Configuration"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. MVC Configuration

스프링은 `WebMvcConfigurer` 라는 인터페이스 제공하여, 애플리케이션 개발자가 쉽게 **MVC 설정을 커스터마이징**할 수 있도록 합니다.      
`WebMvcConfigurer` 의 메서드를 확인해보면 **어떤 항목을 설정**할 수 있는지 확인할 수 있습니다.

이 문서에서는 뷰 컨트롤러 매핑, 인터셉터 추가, `ArgumentResolver` 추가를 학습합니다.

## 참조

- [Spring - MVC Config](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config.html)
- [Be careful when using @Configuration classes with @EnableWebMvc in Spring Boot](https://dev.to/xterm/be-careful-when-using-configuration-classes-with-enablewebmvc-in-spring-boot-2n32)

<br>

# 2. View Controller

`WebMvcConfigurer` 가 제공하는 `addViewControllers` 메서드를 통해 **특정 요청에 대해 뷰를 응답하도록 설정**할 수 있습니다.      
`addViewControllers` 메서드를 사용하면 컨트롤러를 작성하지 않고도 뷰를 응답할 수 있습니다.

## 학습 테스트

- 테스트 메서드: `cholog.WebMvcConfigurationTest.addViewControllers`
- 수행 방법
    - `cholog.config.WebMvcConfiguration.addViewControllers` 을 이용하여 학습 테스트를 성공시키세요.

<br>

기존 "/" 요청 시 index.html 페이지가 응답된다.

`addViewControllers`를 통해 index.html 대신 hello.html 페이지가 응답되게 한다.


## 참조

- [Spring - View Controller](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/view-controller.html)

## 더 생각해보기

- `WebMvcConfigurer` 를 사용하는 방식과 직접 Controller 를 작성하는 방식 중 어떤 방식이 더 좋을까요? 그렇게 생각하는 이유는 무엇인가요?

<details>
<summary>ChatGPT</summary>
<div markdown="1">

### WebMvcConfigurer를 사용하는 방식
    
**장점:**

1. **전역 설정 가능:** WebMvcConfigurer를 사용하면 애플리케이션 전반에 걸친 전역 설정을 손쉽게 정의할 수 있습니다. 예를 들어, CORS 설정, 메시지 컨버터 설정, 인터셉터 추가 등을 간단하게 설정할 수 있습니다.
2. **재사용성:** 여러 컨트롤러에 공통으로 적용되어야 하는 설정을 한 곳에서 관리할 수 있어 코드의 재사용성과 유지보수성이 높아집니다.
3. **관심사 분리:** 컨트롤러는 비즈니스 로직에 집중하고, WebMvcConfigurer는 웹 구성에 집중할 수 있어 코드의 관심사를 분리할 수 있습니다.

**단점:**

1. **세밀한 제어 어려움:** 특정 컨트롤러나 특정 요청에만 적용되어야 하는 설정을 정의하기에는 부적합할 수 있습니다.
2. **복잡성 증가:** 설정이 많아지면 WebMvcConfigurer 클래스가 복잡해질 수 있습니다.

### 직접 Controller를 작성하는 방식

**장점:**

1. **세밀한 제어 가능:** 각 컨트롤러에서 특정한 설정이나 로직을 정의할 수 있어 세밀한 제어가 가능합니다.
2. **간결성:** 간단한 애플리케이션에서는 WebMvcConfigurer를 사용하지 않고 각 컨트롤러에서 직접 로직을 작성하는 것이 더 간단할 수 있습니다.

**단점:**

1. **중복 코드 발생:** 여러 컨트롤러에서 동일한 설정이나 로직이 필요할 경우, 코드 중복이 발생할 수 있습니다.
2. **유지보수 어려움:** 공통 로직이나 설정이 분산되어 있으면 유지보수가 어려워질 수 있습니다.

### 결론

**WebMvcConfigurer를 사용하는 것이 더 좋은 경우:**

- 애플리케이션 전반에 걸쳐 일관된 설정이 필요할 때
- 여러 컨트롤러에 공통된 설정이나 로직을 적용해야 할 때
- 관심사를 분리하여 코드의 가독성과 유지보수성을 높이고 싶을 때

**직접 Controller를 작성하는 것이 더 좋은 경우:**

- 특정 컨트롤러에만 적용되는 특수한 설정이나 로직이 필요할 때
- 간단한 애플리케이션에서 설정이 복잡하지 않고, 빠르게 개발하고자 할 때

</div>
</details>

<br>

# 3. Interceptor

Spring Framework에서 **Interceptor**는 주로 HTTP 요청의 사전 처리와 사후 처리를 관리하는 데 사용되는 컴포넌트입니다.      
Interceptor를 사용해 컨트롤러로 요청을 전달하기 전이나 후에 특정 로직을 실행할 수 있습니다.

`WebMvcConfigurer` 가 제공하는 `addInterceptor` 메서드를 통해 특정 패턴에 대해 인터셉터가 동작하도록 설정할 수 있습니다.

## 학습 테스트

- 테스트 메서드: `cholog.WebMvcConfigurationTest.addInterceptors`
- 수행 방법
    - `cholog.config.WebMvcConfiguration.addInterceptors` 을 이용하여 학습 테스트를 성공시키세요.
        - 회원이 아닌 사람이 회원 목록 조회 요청을 하면 권한이 없다는 응답이 나와야 합니다.
        - `CheckLoginInterceptor` 를 사용하여 요청 규약을 지킨 요청에만 응답하도록 설정하세요.
    - `CheckLoginInterceptor`, `MemberController` 에 breakpoint 를 설정하여 디버깅을 진행하며 작동 순서를 확인해 보세요.

<br>

권한이 없다 = 401 상태 코드

```java
public class CheckLoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {}
}
```

`addInterceptors` 가 preHandle을 먼저 실행 이후 컨트롤러 요청

<img width="1440" alt="Untitled" src="https://github.com/user-attachments/assets/e5795cd8-c1ab-4140-a4ee-b8ec0048384c">

## 참조

- [Spring - DispatcherServlet > Interception](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/handlermapping-interceptor.html)
- [Spring - MVC Config > Interceptors](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/interceptors.html)

## 더 생각해보기

- 스프링이라는 프레임워크가 `HandlerInterceptor` 라는 인터페이스를 제공하고, 이런 행위를 지원하는 이유는 무엇일까요?
- 어떤 상황에서 Interceptor 를 사용할 수 있을까요?

<details>
<summary>ChatGPT</summary>
<div markdown="1">

### 1. **관심사의 분리 (Separation of Concerns)**
    
- 인터셉터는 공통적인 작업(예: 인증, 로깅, 요청 변환 등)을 중앙 집중적으로 처리할 수 있도록 하여 비즈니스 로직과 인프라 로직을 분리합니다. 이를 통해 각 로직의 응집도를 높이고, 코드의 가독성과 유지보수성을 향상시킬 수 있습니다.

### 2. **재사용성 및 모듈화 (Reusability and Modularity)**

- 인터셉터는 애플리케이션의 여러 부분에서 공통적으로 사용되는 기능을 모듈화할 수 있습니다. 한 번 구현한 인터셉터를 여러 곳에서 재사용함으로써 코드 중복을 줄일 수 있습니다.

### 3. **사전 및 사후 처리 (Pre- and Post-processing)**

- 인터셉터는 요청 처리 전후에 특정 작업을 수행할 수 있도록 합니다. `preHandle` 메서드는 컨트롤러가 실행되기 전에, `postHandle` 메서드는 컨트롤러가 실행된 후, `afterCompletion` 메서드는 요청 완료 후에 실행됩니다. 이를 통해 다양한 시점에서 필요한 작업을 수행할 수 있습니다.

### 4. **요청 및 응답 가로채기 (Request and Response Interception)**

- 요청 및 응답을 가로채서 특정 조건에 따라 처리 흐름을 제어할 수 있습니다. 예를 들어, 특정 조건에 따라 요청을 차단하거나, 응답을 수정할 수 있습니다.

### 5. **AOP와의 통합 (Integration with Aspect-Oriented Programming)**

- 스프링의 인터셉터는 AOP(Aspect-Oriented Programming) 패러다임과 유사한 기능을 제공합니다. 특정 지점에서 공통 로직을 실행함으로써 AOP의 장점을 활용할 수 있습니다.

### **인터셉터를 사용할 수 있는 상황들:**

1. **인증 및 권한 부여 (Authentication and Authorization)**
  - 특정 요청이 인증되었는지 확인하거나, 사용자가 요청을 수행할 권한이 있는지 확인할 때 인터셉터를 사용할 수 있습니다. 예를 들어, 로그인 여부를 확인하고, 로그인되지 않은 사용자는 로그인 페이지로 리디렉션할 수 있습니다.
2. **로깅 및 감사 (Logging and Auditing)**
  - 요청 및 응답 정보를 로깅하거나, 감사 로그를 작성할 때 인터셉터를 사용할 수 있습니다. 예를 들어, 모든 요청의 URI, HTTP 메서드, 요청 시간을 로깅할 수 있습니다.
3. **성능 모니터링 (Performance Monitoring)**
  - 요청 처리 시간을 측정하여 성능을 모니터링할 수 있습니다. 요청 시작 시간과 종료 시간을 기록하여 처리 시간을 계산할 수 있습니다.
4. **요청 데이터 변환 (Request Data Transformation)**
  - 요청 데이터의 전처리 작업을 수행할 수 있습니다. 예를 들어, 요청 파라미터를 검증하거나, 특정 형식으로 변환할 수 있습니다.
5. **응답 데이터 변환 (Response Data Transformation)**
  - 응답 데이터를 후처리하여 클라이언트에 반환하기 전에 수정할 수 있습니다. 예를 들어, 응답 데이터에 공통적인 헤더를 추가하거나, 특정 조건에 따라 응답 데이터를 변환할 수 있습니다.
6. **캐싱 (Caching)**
  - 특정 요청의 결과를 캐싱하여 동일한 요청에 대해 빠르게 응답할 수 있도록 할 때 인터셉터를 사용할 수 있습니다.

</div>
</details>

<br>    

# 4. Argument Resolver

Spring Framework에서 `HandlerMethodArgumentResolver`는 **요청 데이터를 메서드의 매개변수로 변환**할 때 사용하는 전략 인터페이스입니다.       
컨트롤러의 메서드가 호출될 때 **매개변수에 전달할 객체를 생성하거나 조작하는 로직을 구현**할 수 있습니다.     

예를 들어, HTTP 요청의 특정 헤더를 객체로 변환하거나, 세션에서 사용자 정보를 가져와 매개변수에 주입하는 등의 작업을 수행할 수 있습니다.

`WebMvcConfigurer` 가 제공하는 `addArgumentResolvers` 메서드를 통해 커스텀 ArgumentResolver를 추가할 수 있습니다.

## 학습 테스트

- 테스트 메서드: `cholog.WebMvcConfigurationTest.addArgumentResolvers`
- 수행 방법
    - `cholog.config.WebMvcConfiguration.addArgumentResolvers` 을 이용하여 학습 테스트를 성공시키세요.
        - `GET /favorites` 요청 시, 컨트롤러에서 `LoginMember`를 인자로 받을 수 있도록 설정하세요.

<br>

`LoginMember` 를 리턴하는 `resolveArgument` 함수를 갖는 `AuthenticationPrincipalArgumentResolver` 클래스를 resolvers로 등록한다.

```java
resolvers.add(new AuthenticationPrincipalArgumentResolver());
```

## 참조

- [Handler Method Argument Resolver](https://www.baeldung.com/spring-mvc-custom-data-binder#1-custom-argument-resolver)

## 더 생각해보기

- 스프링이라는 프레임워크가 `HandlerMethodArgumentResolver` 라는 인터페이스를 제공하고, 이런 행위를 지원하는 이유는 무엇일까요?
- 어떤 상황에서 ArgumentResolver 를 사용할 수 있을까요?

<details>
<summary>ChatGPT</summary>
<div markdown="1">

### 스프링이 `HandlerMethodArgumentResolver`를 제공하는 이유
    
1. **컨트롤러 메서드의 매개변수 처리 유연성:**
    - `HandlerMethodArgumentResolver`는 컨트롤러 메서드의 매개변수를 유연하게 처리할 수 있도록 합니다. 이를 통해 개발자는 요청의 다양한 부분에서 데이터를 추출하여 컨트롤러 메서드에 전달할 수 있습니다.
2. **사용자 정의 매개변수 주입:**
    - 기본적으로 스프링은 여러 가지 표준 매개변수 타입(예: `HttpServletRequest`, `HttpServletResponse`, `Model`, `Principal` 등)을 지원하지만, `HandlerMethodArgumentResolver`를 사용하면 사용자 정의 객체를 컨트롤러 메서드에 주입할 수 있습니다.
3. **비즈니스 로직 분리:**
    - 매개변수 주입 로직을 컨트롤러 메서드에서 분리하여 더 깔끔하고 관리하기 쉬운 코드를 작성할 수 있습니다. 이를 통해 컨트롤러 메서드는 비즈니스 로직에 집중할 수 있습니다.
4. **재사용 가능한 코드 작성:**
    - 공통적인 매개변수 처리 로직을 별도의 Resolver로 분리하여 여러 컨트롤러에서 재사용할 수 있습니다. 이를 통해 코드 중복을 줄이고 유지보수성을 높일 수 있습니다.

### `HandlerMethodArgumentResolver`를 사용할 수 있는 상황

1. **인증된 사용자 정보 주입:**
    - 예를 들어, JWT 토큰이나 세션을 통해 인증된 사용자 정보를 `LoginMember`와 같은 객체로 변환하여 컨트롤러 메서드에 주입할 때 사용합니다.
2. **특정 헤더나 쿠키 값 추출:**
    - 요청 헤더나 쿠키에서 값을 추출하여 특정 객체에 바인딩하는 경우 사용할 수 있습니다.
3. **복잡한 요청 매개변수 처리:**
    - 요청 매개변수의 복잡한 조합을 처리하여 도메인 객체로 변환하거나, 여러 매개변수를 조합하여 하나의 객체로 전달할 때 유용합니다.
4. **다양한 요청 소스에서 데이터 추출:**
    - 요청 본문, 경로 변수, 쿼리 파라미터 등 다양한 요청 소스에서 데이터를 추출하여 컨트롤러 메서드 매개변수에 바인딩할 수 있습니다.

</div>
</details>

<br>

# 코드

[https://github.com/KimGyeongLock/spring-learning-test/blob/roki/spring-mvc-4/spring-mvc-4/initial/src/main/java/cholog/config/WebMvcConfiguration.java](https://github.com/KimGyeongLock/spring-learning-test/blob/roki/spring-mvc-4/spring-mvc-4/initial/src/main/java/cholog/config/WebMvcConfiguration.java)
