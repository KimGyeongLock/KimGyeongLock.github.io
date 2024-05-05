---
layout: single
title: Spring2 (Controller)
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

## Spring의 기본구조

MVC (Model-View-Controller) 패턴

![Untitled](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/002e008f-c569-4d2f-9636-f90caded04de)

*chatGPT:*

1. **Controller (컨트롤러)**:
    - 클라이언트의 요청을 받고 적절한 처리를 위해 서비스 계층에 작업을 위임합니다.
    - 주로 HTTP 요청을 처리하고, **요청된 데이터를 적절한 서비스 메서드에 전달**하여 비즈니스 로직을 수행합니다.
    - 일반적으로 웹 애플리케이션의 엔드포인트를 정의하고, **클라이언트에게 응답을 제공**합니다.
2. **Service (서비스)**:
    - 비즈니스 **로직을 처리**합니다.
    - 일반적으로 여러 컨트롤러에서 사용되는 공통 로직이나 데이터 조작을 수행합니다.
    - 서비스는 컨트롤러로부터 데이터를 받아 비즈니스 로직을 수행하고, 결과를 컨트롤러에게 반환합니다.
3. **DAO (Data Access Object, 데이터 접근 객체)**:
    - **데이터베이스와의 상호 작용**을 담당합니다.
    - 주로 데이터베이스와의 통신을 추상화하고, 데이터베이스로부터 데이터를 검색, 저장, 갱신 및 삭제하는 작업을 수행합니다.
    - DAO는 데이터 엔터티에 대한 접근을 캡슐화하여 서비스 계층이 데이터베이스의 구체적인 세부 사항에 의존하지 않도록 합니다.
4. **Repository (리포지토리)**:
    - 일반적으로 Spring Data JPA와 같은 ORM(Object-Relational Mapping) 프레임워크를 사용할 때 사용됩니다.
    - 데이터베이스 조작을 추상화하고, JPA(Entity Manager)를 사용하여 **데이터를 저장, 검색, 갱신, 삭제**합니다.
    - Repository는 DAO의 일종으로 생각할 수 있으며, Spring Data JPA가 제공하는 기능을 이용하여 개발자가 쉽게 데이터베이스 조작을 수행할 수 있도록 합니다.
5. **Mapper**:
    - 주로 MyBatis와 같은 SQL 매핑 프레임워크에서 사용됩니다.
    - 객체와 데이터베이스 레코드 간의 **매핑 작업**을 처리합니다.
    - SQL 쿼리를 실행하고, 결과를 객체로 매핑하거나, 객체를 SQL 쿼리의 파라미터로 매핑합니다.

## Controller vs RestController

1. `@Controller`
    - **페이지 이동**이 발생하는 컨트롤러
    - ***thymeleaf***를 함께 사용
    - 웹 페이지 이동하는 것과 생각하면 비슷

1. `@RestController`
    - **페이지 이동없이**, 정보를 받아올 수 있는 구조
    - api와 비슷

### IndexPageController.java

```sql
@Controller //페이지 전환을 위한 컨트롤러!!
//@RequestMapping("/page")
public class IndexPageController {
    @GetMapping("/index") 
    public String index(){
        return "index";
    }
    @GetMapping("/test")
    public String test(){
        return "test";
    }

    @GetMapping("/check")
    public String check(@RequestParam(required = false) String id, @RequestParam(required = false) String pw, Model model){
        System.out.println("id : " + id);
        System.out.println("pw : " + pw);
        //
        //아이디와 패스워드르 확인하는 무언가의 기능
        model.addAttribute("result", id + " / 로그인 성공");
        return "check";
    }
    @GetMapping("/check2") //map으로 parameter 줄이기
    public String check2(@RequestParam Map<String, Object> map, Model model){
        System.out.println("id : " + map.get("id")); //id : value1
        System.out.println("pw : " + map.get("pw")); //pw : value2
        //
        //아이디와 패스워드르 확인하는 무언가의 기능
        model.addAttribute("result", map.get("id") + " / 로그인 성공!");
        return "check2";
    }
}
```

- ex) http://localhost:8080/check2?**id=aa**&**pw=1234**
    
    <img width="473" alt="Untitled 1" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/7c4a72ad-5713-4745-83a7-9836b05cdfcf">
    

```html
<html lang="ko" xmlns:th="http://www.thymeleaf.org">
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
Hello! <b style="background-color:yellow;">hahah</b>INDEX!!!

id2 : <input type="text" th:value="${result}">
</body>
</html>
```

- View에서 ’name’(”`result`”)으로 지정된 value(”`map.get("id") + " / 로그인 성공!"`”)를 사용

---

### IndexRestController.java

```sql
@RestController
@RequestMapping("/api")
public class IndexRestController {
    @GetMapping("/index")
    public String index(@RequestParam String params){
        System.out.println("params : " + params);
        return "index";
    }
    @GetMapping("/test")
    public String test(){
        return "test";
    }
}
```

1. `@RequestMapping(’/~~~’)`
    - URL로 들어온 요청과 특정 method를 매핑하기 위해 사용하는 Annotation
    - 공통 url
2. `@GetMapping(’/~~~’)`
    - HTTP Get Method에 해당하는 단축 표현으로 서버의 리소스를 조회할 때 사용
    - 컨트롤러를 부르는 주소(~~~)는 unique
    - Get 방식
        - URL에 데이터를 포함시켜 요청
        - 데이터를 헤더에 포함하여 전송
        - URL에 데이터가 노출되어 보안에 취약
        - 캐싱할 수 있음
        
        => 주로 조회할때만 사용
        
3. `@RequestParam(,,)`
    - HTTP 요청 파라미터 받아오기

## 궁금증

- ***thymeleaf란?***
    - View Template(뷰 템플릿)
        - 컨트롤러가 전달하는 데이터를 이용하여 동적으로 화면을 구성할 수 있게 해줍니다
    - html태그를 기반으로하여 th:속성을 이용하여 동적인 View를 제공
    
- ***controller와 restController 차이***
