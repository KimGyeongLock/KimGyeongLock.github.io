---
layout: single
title: "[Spring-MVC-2] API CRUD와 HTTP Status"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. CRUD API

CRUD는 대부분의 소프트웨어가 가지는 기본적인 데이터 처리 기능으로, Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 의미하는 말입니다.    
리소스를 관리하는 일반적인 API를 만들 때 역시 CRUD 기능을 구현합니다.     

# 2. create

리소스 생성을 요청하는 API입니다.     
서버에 데이터를 제출하기 위해 **POST 메서드**를 사용합니다.     
리소스 생성 시 필요한 데이터를 json 형태로 body에 담아 요청을 보냅니다.     

```
POST /members HTTP/1.1
content-type: application/json

{
    "name": "브라운",
    "age": 20
}

```

요청에 성공하면 **201 응답코드**를 응답 받습니다.     
그리고 Location 헤더에 생성된 리소스의 위치를 담아 응답을 받습니다.     
생성된 리소스를 확인할 수 있도록 body에 생성된 리소스를 담아 응답할 수 있습니다.     

```
HTTP/1.1 201
Location: /members/1
Content-Type: application/json

{
    "id": 1,
    "name": "브라운",
    "age": 20
}

```

<br>

- **200(성공):** 서버가 요청을 제대로 처리했다는 뜻이다. 이는 주로 서버가 요청한 페이지를 제공했다는 의미로 쓰인다.
- **201(작성됨):** 성공적으로 요청되었으며 서버가 새 리소스를 작성했다.
- **204(콘텐츠 없음):** 서버가 요청을 성공적으로 처리했지만 콘텐츠를 제공하지 않는다.

출처: [https://ko.wikipedia.org/wiki/HTTP_상태_코드](https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C)
<br>

## 학습 테스트

- 테스트 메서드: `cholog.CRUDTest.create`
- 수행 방법
    - `cholog.MemberController.create` 을 이용하여 학습 테스트를 성공시키세요.

<br>

```java
public ResponseEntity<Void> create(@RequestBody Member member) {}
```

- `@RequestBody` 어노테이션을 사용하면 HTTP 요청 본문의 JSON 데이터가 자동으로 `Member` 객체로 변환

```java
return ResponseEntity.created(URI.create("/members/" + newMember.getId())).build();
```

- `"/members/" + newMember.getId()` == `/members/1`
- `ResponseEntity.created(location).build();`
    - 201 응답코드
    - Create a new builder with a CREATED status and a location header set to the given URI.

<br>

## 참조

- [Spring - ResponseEntity](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/responseentity.html)
- [Spring - @RequestBody](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/requestbody.html)

# 3. read

리소스 조회를 요청하는 API입니다.     
서버에 리소스의 정보를 검색하기 위해 **GET 메서드**를 사용합니다.     

```
GET /members HTTP/1.1

```

요청에 성공하면 **200 응답코드**를 응답 받습니다.     
조회된 정보를 body에 담아 응답할 수 있습니다.     

```
HTTP/1.1 200
Content-Type: application/json

[
    {
        "id": 1,
        "name": "브라운",
        "age": 20
    },
    {
        "id": 2,
        "name": "브리",
        "age": 10
    }
]

```

## 학습 테스트

- 테스트 메서드: `cholog.CRUDTest.read`
- 수행 방법
    - `cholog.MemberController.read` 을 이용하여 학습 테스트를 성공시키세요.

<br>
```java
return ResponseEntity.ok().body(members);
return ResponseEntity.ok(members);
```

- `ok()` : HTTP 상태 코드 200(OK)


# 4. update

리소스 수정을 요청하는 API입니다.     
리소스를 대체하기 위해 **PUT 메서드**를 사용합니다.       
PATCH를 이용할 수 있으나 전체 리소스를 대체하기 위해 PUT을 사용합니다.       
**수정할 리소스의 식별자를 url path에 포함**해서 요청을 보냅니다.       
body 값에는 수정할 정보를 담아서 보냅니다.       

```

PUT /members/1 HTTP/1.1

{
    "name": "브라운",
    "age": 30
}

```

요청에 성공하면 **200 응답코드**를 응답 받습니다.

```
HTTP/1.1 200

```

## 학습 테스트

- 테스트 메서드: `cholog.CRUDTest.update`
- 수행 방법
    - `cholog.MemberController.update` 메서드를 작성하여 학습 테스트를 성공시키세요.

<br> 

```java
@PutMapping("/members/{id}")
public ResponseEntity<Void> update(@PathVariable Long id, @RequestBody Member info) {}
```

- `@PathVariable("id")`  == `@PathVariable(name = "id") Long id` == `@PathVariable Long id`
    - {id} ⇒ id
    - URL 경로에서 변수 값을 추출하여 매개변수에 할당한다.
- `ResponseEntity.*ok*().build()`
    - Void → .build()!


## 참조

- [Spring - Method Arguments > @PathVariable](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/arguments.html)

# 5. delete
  
리소스 삭제를 요청하는 API입니다.         
리소스를 삭제하기 위해 **DELETE 메서드**를 사용합니다.        
삭제할 리소스의 **식별자**를 url path에 포함해서 요청을 보냅니다.         

```
DELETE /members/1 HTTP/1.1

```

요청에 성공하면 **204 응답코드**를 응답 받습니다.

```
HTTP/1.1 204

```

## 학습 테스트

- 테스트 메서드: `cholog.CRUDTest.delete`
- 수행 방법
    - `cholog.MemberController.delete` 메서드를 작성하여 학습 테스트를 성공시키세요.

<br>
```java
return ResponseEntity.noContent().build();
```

- 204 응답코드
