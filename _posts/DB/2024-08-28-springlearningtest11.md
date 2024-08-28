---
layout: single
title: "[Spring-AUTH-1] Basic Auth, Session Login, Token Login"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Basic Auth

![basic](https://github.com/user-attachments/assets/a809a9a9-5bf7-4330-aba3-76dd70c30d2b)

기본 인증(Basic Authentication) 방식은 사용자의 아이디와 비밀번호를 웹 사이트에 알려주는 간단한 방법입니다.    
사용자 이름과 비밀번호를 **웹 브라우저에서 서버**로 보낼 때는 `Authorization: Basic <credentials>`라는 형태로 요청 **헤더에 정보를 실어 보냅니다.**    
여기서 `<credentials>` 부분에는 **사용자의 아이디와 비밀번호를 콜론 하나로 이어붙인 문자열**(`{{userName}}:{{password}}`)을 **Base64라는 방식으로 인코딩**합니다.    
실제로 보내지는 정보는 **Base64로 인코딩된 문자열 형태**로 전송되어, 직접 눈으로 봤을 때는 사용자 이름이나 비밀번호를 쉽게 알아볼 수 없습니다.    

```
Headers: Authorization=Basic ZW1haWxAZW1haWwuY29tOjEyMzQ=
```

정리    

"ZW1haWxAZW1haWwuY29tOjEyMzQ=" - **Base64**

\{\{userName\}\}:\{\{password\}\} 가 인코딩되어 있다.

**RestAssured(테스트용)**를 사용해 Basic Auth를 적용하려면,    
아래와 같이 테스트 코드에 인증 정보를 포함해 Authorization 헤더를 자동으로 설정하도록 작성합니다.    

```java
.auth().preemptive().basic(EMAIL, PASSWORD)
```

`.auth().preemptive().basic()`

- **Preemptive Authentication**: 이 방식은 서버가 인증 요청을 요구하기 전에 클라이언트가 먼저 인증 정보를 서버로 전송하는 것입니다. 즉, 클라이언트가 서버에 첫 요청을 보낼 때, 인증 헤더를 포함시켜서 요청을 보냅니다.
- **장점**:
    - **속도**: 서버로부터 401 Unauthorized 응답을 기다릴 필요 없이, 첫 요청에서 바로 인증을 수행하므로 응답 시간을 단축시킬 수 있습니다.
    - **단점**:
        - **보안**: 인증 정보를 항상 모든 요청에 포함시키기 때문에, 필요 없는 경우에도 인증 정보를 노출할 위험이 있습니다.

`.auth().basic()`

- **Challenged Authentication**: 이 방식은 서버가 클라이언트에게 401 Unauthorized 응답을 보낸 후에 클라이언트가 인증 정보를 서버로 전송하는 방식입니다. 즉, 클라이언트가 서버로 처음 요청을 보낼 때는 인증 정보를 포함하지 않으며, 서버가 인증이 필요하다고 판단하여 401 응답을 보내면 그때 인증 정보를 전송합니다.
- **장점**:
    - **보안**: 불필요한 요청에 인증 정보를 포함하지 않으므로, 인증 정보의 불필요한 노출을 줄일 수 있습니다.
    - **단점**:
        - **속도**: 클라이언트가 401 응답을 받은 후에 다시 인증 정보를 포함하여 요청을 보내기 때문에, 첫 요청 시에는 응답 시간이 길어질 수 있습니다.

Authorization 헤더에 담긴 정보를 추출하는 방법은 아래와 같습니다.

```java
AuthInfo authInfo = authorizationExtractor.extract(request);
```

ex) request sample

```
GET /members/me/basic HTTP/1.1
authorization: Basic ZW1haWxAZW1haWwuY29tOjEyMzQ=
accept: application/json
```

## 참조

- [`@RequestParam` or `HttpServletRequest`](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-arguments)

-------

# 2. Session Login

<img width="702" alt="session" src="https://github.com/user-attachments/assets/5df0b8a3-0256-4021-8b5c-08a03594c307">

Basic Authentication 방식의 경우 **매 요청마다 아이디와 패스워드를 전송**하는데, **보안상으로 문제**가 있을 수 있고 효율적이지 않습니다.    
**세션 기반 로그인 방식**은 사용자가 첫 로그인 시에만 신원 정보를 제출하고, 서버는 이를 확인한 뒤 **세션 ID를 발급**하여 응답합니다.    
사용자는 이후의 요청에서 이 **세션 ID를 사용하여 자신을 인증**하고, 서버는 이를 통해 사용자의 로그인 상태를 식별하고 유지합니다.    
세션 ID를 이용함으로써 **매 요청시마다 신원을 증명하는 부담을 줄일 수 있습니다.**    

세션 ID 응답은 **Set-Cookie 헤더**에 담겨서 응답됩니다.    

```
HTTP/1.1 200
Set-Cookie: JSESSIONID=89EA9B9B9F00EAC2B8D2208649EA6260; Path=/; HttpOnly
```

이후 요청에는 **Cookie 헤더**에 세션 ID를 담아서 요청합니다.

```
Headers: Cookie=JSESSIONID=89EA9B9B9F00EAC2B8D2208649EA6260
```

ex) request sample (사용자 로그인 요청)

```
POST /login/session HTTP/1.1
content-type: application/x-www-form-urlencoded; charset=ISO-8859-1
host: localhost:55477

email=email@email.com&password=1234
```

ex) request sample (이후 리소스 요청)

```
GET /members/me/session HTTP/1.1
cookie: JSESSIONID=E7263AC9557EF658C888F02EEF840A19
accept: application/json
```

## HttpRequest로 받은 email과 password 추출

- **getParameter(String name)**: 특정 파라미터의 값을 문자열로 반환합니다. 파라미터가 여러 개일 경우 첫 번째 값을 반환합니다.
- **getParameterValues(String name)**: 특정 파라미터의 값을 배열로 반환합니다. 파라미터가 여러 개일 경우 모두 반환합니다.
- **getParameterMap()**: 모든 파라미터를 키-값 쌍의 맵(Map) 형태로 반환합니다. 여기서 키는 파라미터의 이름이고, 값은 해당 파라미터 값들의 배열입니다.
    
    ```java
    {
    	"email": ["[email@email.com](mailto:email@email.com)"],
    	"password": ["1234"]
    }
    ```
    
    - `String email = paramMap.get(USERNAME_FIELD)[0];`
    - `String password = paramMap.get(PASSWORD_FIELD)[0];`

## Session에 인증 정보 저장

`session.setAttribute("SESSION_KEY", email);`

## Session을 통해 인증 정보 조회

`session.getAttribute("SESSION_KEY")`

## 참조

- [HttpSession](https://www.baeldung.com/spring-security-session#2-injecting-the-raw-session-into-a-controller)

-------

# 3. Token Login

<img width="508" alt="token" src="https://github.com/user-attachments/assets/c88171a8-154b-4cfc-9d2e-11b5aa7edbc0">

토큰 기반 로그인 방식에서 사용자는 **최초 로그인 때 아이디와 패스워드 같은 신원 정보를 포함해서 요청**합니다. (세션과 동일)    
서버는 이 정보를 검증한 후, **암호화된 접근 토큰**(Access Token, 예: **JWT**)을 발급하여 응답합니다.    

- ***JWT:*** Json Web Token의 약자로 json객체를 이용해서 토큰 자체의 정보를 저장하고 있는 웹 토큰

사용자는 이후의 요청에 이 **토큰을 포함시켜 자신을 인증**하게 되며,    
서버는 요청이 들어올 때마다 **헤더에 포함된 토큰을 검증**하여 사용자의 신원을 확인하고 접근 권한을 제어합니다.    

토큰 발급 이후, 서버로 보내는 요청에는 토큰값은 담아서 보내는데 **Authorization 헤더**에 담아서 보냅니다.    

```
Headers: Authorization=Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJlbWFpbEBlbWFpbC5jb20iLCJpYXQiOjE3MDU4NDU2NzIsImV4cCI6MTcwNTg0OTI3Mn0.YibLSi-PenIMc0LJUW50A_hq98uZmQu7OAdIxIvF4MY
```

ex) request sample (사용자 로그인 요청)

```
POST /login/token HTTP/1.1
accept: application/json
content-type: application/json; charset=UTF-8

{
  "email": "email@email.com",
  "password": "1234"
}
```

- `@RequestBody` 를 통해 email, password 정보를 가져옴
- TokenRequest class를 사용해서 email과 password를 묶음
- `@RequestBody TokenRequest tokenRequest`

ex) request sample (이후 리소스 요청)

```
GET /members/me/token HTTP/1.1
authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJlbWFpbEBlbWFpbC5jb20iLCJpYXQiOjE2MTAzNzY2NzIsImV4cCI6MTYxMDM4MDI3Mn0.Gy4g5RwK1Nr7bKT1TOFS4Da6wxWh8l97gmMQDgF8c1E
accept: application/json
```

- authorization 헤더에 포함되기 때문에 `authorizationExtractor` 를 사용
- `String token = authorizationExtractor.extract(request);`

-------

# 각 로그인별 특징과 차이점

## 1. **Basic Authentication**

- **특징**:
    - **간단한 인증 방식**: 사용자 이름과 비밀번호를 Base64로 인코딩한 후 `Authorization` 헤더에 포함하여 서버에 전달합니다.
    - **보안 문제**: Base64 인코딩은 암호화가 아니며, HTTPS 없이 전송할 경우 중간에서 **쉽게 탈취**될 수 있습니다.
    - **스테이트리스(stateless)**: 서버는 **상태를 유지**하지 않습니다. **각 요청에서 사용자 자격 증명을 포함**해야 합니다.
    - **간단한 구현**: 클라이언트와 서버 모두에서 구현이 쉽습니다.
- **장점**:
    - 간단하고, 대부분의 HTTP 클라이언트와 서버가 기본적으로 지원합니다.
    - 추가적인 상태 관리를 하지 않으므로 서버 측에서의 부담이 적습니다.
- **단점**:
    - 모든 요청에서 자격 증명이 전송되므로, **보안상 위험**할 수 있습니다.
    - 자격 증명을 자주 전송하기 때문에, HTTPS를 사용하지 않으면 안전하지 않습니다.
- **사용 예**: 단순한 API 접근이나 테스트 용도로 사용될 수 있습니다.

## 2. **Session Login**

- **특징**:
    - **세션 기반 인증**: 클라이언트가 로그인하면 서버는 사용자에 대한 세션을 생성하고, 세션 ID를 쿠키로 클라이언트에 전송합니다.
    - **상태 유지(Stateful)**: 서버가 **세션 상태를 유지**하며, 클라이언트는 이후 요청에서 세션 ID를 포함한 쿠키를 전송하여 인증을 받습니다.
    - **세션 관리**: 서버는 세션 정보를 관리해야 하며, **메모리 또는 데이터베이스에 세션 데이터를 저장**합니다.
    - **일반적인 웹 애플리케이션**: 대부분의 **전통적인** 웹 애플리케이션에서 사용됩니다.
- **장점**:
    - 세션이 서버에서 관리되므로 보안이 강화됩니다. 자격 증명이 클라이언트에 저장되지 않고, 세션 ID가 주기적으로 갱신될 수 있습니다.
    - 로그아웃 기능이 쉬워집니다. **서버에서 세션을 무효화하면 클라이언트의 인증이 해제**됩니다.
- **단점**:
    - 서버가 상태를 유지해야 하므로, **스케일링이 어려울 수 있습니다.**
    - 세션 데이터가 서버에 저장되므로, **서버 간 세션 동기화**가 필요할 수 있습니다.
- **사용 예**: 대부분의 웹 애플리케이션, 특히 사용자 로그인 세션이 필요한 경우.

## 3. **Token Authentication (예: JWT, OAuth)**

- **특징**:
    - **토큰 기반 인증**: 사용자가 로그인하면 서버는 JSON Web Token (JWT)과 같은 토큰을 생성하여 클라이언트에 전달합니다. 클라이언트는 이후 요청에 이 토큰을 포함하여 서버에 전송합니다.
    - **스테이트리스(stateless)**: 서버는 **상태를 유지하지 않으며**, 토큰 자체에 사용자의 인증 정보가 포함됩니다.
    - **보안**: 토큰은 서명되어 있어, **데이터가 변조되지 않았음을 보장**할 수 있습니다. 토큰의 만료 시간을 설정할 수 있어 **추가적인 보안**을 제공합니다.
- **장점**:
    - 서버는 상태를 유지하지 않으므로, 확장성 있는 시스템 구축이 가능합니다.
    - 토큰에 다양한 정보(클레임)를 담을 수 있어 유연성이 높습니다.
    - 클라이언트가 토큰을 로컬에 저장하고 사용할 수 있으므로, 지속적인 인증이 가능합니다.
- **단점**:
    - 토큰이 클라이언트에 저장되므로, 이 저장소가 안전하지 않으면 보안에 취약할 수 있습니다.
    - 토큰이 만료되기 전까지는 서버에서 강제로 로그아웃시키기 어렵습니다.
- **사용 예**: RESTful API, 모바일 애플리케이션, SPA(Single Page Application) 등에서 널리 사용됩니다.
