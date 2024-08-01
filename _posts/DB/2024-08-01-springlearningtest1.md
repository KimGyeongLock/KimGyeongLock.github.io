---
layout: single
title: "[Spring-MVC-1] static과 templates, @RequestParam, @ResponseBody"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Welcome Page

스프링 부트는 **정적 페이지**와 **템플릿 시작 페이지**를 모두 지원합니다.    
먼저 구성된 정적 콘텐츠 위치에서 index.html 파일을 찾습니다.     
하나라도 없으면 index 템플릿을 찾습니다.     
둘 중 하나라도 찾으면 자동으로 응용 프로그램 시작 페이지로 사용됩니다.     

### 파일 경로

```
resources
ㄴ static (정적 페이지)
  ㄴ index.html

or

resources
ㄴ templates (템플릿 시작 페이지)
  ㄴ index.html

```

<span style="color: green">
\[정적 페이지와 템플릿 시작 페이지 무슨 차이인가?\]

`resources/static`는 **정적 리소스**를 저장하는 데 사용되며 정적 리소스에는 HTML, CSS, JavaScript, 이미지 파일 등이 포함된다.

`resources/templates`의 경우 **동적 웹 페이지**를 저장하는 경로로 사용됩니다. 여기에 저장된 HTML 파일은 `Thymeleaf`와 같은 템플릿 엔진을 통해 처리되며, 이 과정에서 서버 측 데이터나 로직이 페이지에 반영되어 최종적인 HTML이 생성됩니다. 

EX) ${data}를 사용하여 서버로부터 data가 무엇인지에 따라 화면에 데이터가 바뀔 수 있음

<https://www.inflearn.com/community/questions/1129544/resources-폴더의-static-폴더와-templates-폴더-차이>
</span>

### 학습 테스트

welcome page 설정을 연습하는 학습 테스트 입니다.

- 테스트 메서드: `cholog.ResponseStaticTest.responseIndexPage`
- 수행 방법
    - `resources/static/hi.html` 을 이용하여 학습 테스트를 성공시키세요.
    - welcome page 설정을 위해 적절한 위치에 이동을 하거나 파일명을 변경해보세요.

<span style="color: green">    

`cholog.ResponseStaticTest.responseIndexPage` 실행시 404 Not Found 에러 발견

<img width="1340" alt="Untitled" src="https://github.com/user-attachments/assets/f2d9df33-f44d-4514-9506-c17e8fbaa9ac">

`/` == `/index.html`  기본 페이지와 같다!

responseIndexPage함수에서 hi.html을 작동하기 위해서는 hi.html의 이름을 index.html로 변경해야 한다.

<img width="1348" alt="Untitled 1" src="https://github.com/user-attachments/assets/297b5ae4-451c-4c02-a883-af0437193098">

Build Success를 확인 

<details>
<summary>또는</summary>
<div markdown="1">

<img width="1078" alt="Untitled 2" src="https://github.com/user-attachments/assets/6555c25b-efb0-47d1-acf5-78625c5b8243">

</div>
</details>

</span>


### 참고자료

- [Spring Boot - Welcome Page](https://docs.spring.io/spring-boot/docs/3.1.2/reference/htmlsingle/#web.servlet.spring-mvc.welcome-page)

# 2 Static Page

resources/static 아래의 경로에 위치한 파일은 접근이 가능합니다.
서비스에서 필요한 정적 자원들을 해당 경로에 위치시킨 후 활용할 수 있습니다.

<span style="color: green">   
Spring Boot는 기본적으로 `src/main/resources/static` 디렉토리에서 정적 리소스를 서빙합니다. 
</span>

### 학습 테스트

정적 페이지 설정을 연습하는 학습 테스트 입니다.

- 테스트 메서드: `cholog.ResponseStaticTest.responseStaticPage`
- 수행 방법
    - `resources/templates/static.html` 을 이용하여 학습 테스트를 성공시키세요.
    - 정적 페이지 설정을 위해 적절한 위치에 이동을 하거나 파일명을 변경해보세요.
    
<span style="color: green">   
`cholog.ResponseStaticTest.responseStaticPage` 실행시 404 Not Found 에러 발견

<img width="462" alt="Untitled 3" src="https://github.com/user-attachments/assets/1657d43e-b0ab-4867-87fb-286758d81ec6">

static.html은 templates 폴더에 위치하여 파일을 찾지 못했다.

static 폴더로 파일을 이동시킨다.

<img width="1072" alt="Untitled 4" src="https://github.com/user-attachments/assets/f6b4292b-fbd6-45b6-a441-214492c080c3">

Build Success를 확인 
</span>

### 참고자료

- [Spring - Static Resources](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/static-resources.html#page-title)


# 3. Template Engine

동적으로 페이지 처리를 하기 위해서는 템플릿 엔진을 활용할 수 있습니다.
이번 학습 테스트에서는 `Thymeleaf`를 활용하여 요청에 대한 동적 처리를 합니다.
쿼리 스트링(?name=brown)으로 전달된 name 값을 `@RequestParam`을 활용하여 **컨트롤러 메서드의 파라미터로 주입** 받습니다.
컨트롤러 메서드 내에서 뷰로 값을 전달하기 위해서 `Model` 객체를 활용합니다.
Model 객체는 **컨트롤러 메서드의 파라미터로 주입** 받을 수 있고, **addAttribute** 메서드를 통해 값을 전달할 수 있습니다.

<span style="color: green">   
\[`@RequestParam`과 `@RequestBody`의 차이\]

@RequestParam은 URL에 요청 파라미터를 바인딩하지만 , @RequestBody는 Http Body에 있는 내용을 Java - Object로 반환합니다.

출처: [https://mooonstar.tistory.com/entry/SpringRequestBody와-RequestParam-비교하여-이해하기](https://mooonstar.tistory.com/entry/SpringRequestBody%EC%99%80-RequestParam-%EB%B9%84%EA%B5%90%ED%95%98%EC%97%AC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0) [MoonStar:티스토리]
</span>

### 학습 테스트

- 테스트 메서드: `cholog.ResponseTemplatesTest.responseTemplatesPage`
- 수행 방법
    - `cholog.MemberController.world` 메서드를 작성하여 학습 테스트를 성공시키세요.
    - `/hello` 요청 시 `resources/templates/hello.html` 페이지가 응답할 수 있도록 설정하세요.

<span style="color: green">   
1. TODO: /hello 요청 시 resources/templates/hello.html 페이지가 응답할 수 있도록 설정하세요.
    - `/hello?name=Brie` 에서 name을 get (받아온다.)
    - `@GetMapping("/hello")` // /hello 요청 시
        - 자동으로 templates 폴더에서 찾는다?
2. TODO: 쿼리 파라미터로 name 요청이 들어왔을 때 해당 값을 hello.html에서 사용할 수 있도록 하세요.
    - 컨트롤러 메서드 내에서 뷰로 값을 전달하기 위해서 `Model` 객체를 활용
    - **addAttribute** 메서드를 통해 값을 전달
    
    ```java
    model.addAttribute("name", name);
    return "hello"; //hello.html에서 사용
    ```
    
- return null 로 해도 된다?? - Spring MVC는 요청 URL을 사용하여 뷰 이름을 결정하려고 시도합니다
</span>

### 참고자료

- [Spring - Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
- [Spring - @RequestParam](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/requestparam.html)
- [Spring - Method Arguments > Model](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/arguments.html)
- [Baeldung - Introduction to Using Thymeleaf in Spring](https://www.baeldung.com/thymeleaf-in-spring-mvc)

# 4. Json 응답

컨트롤러 메서드의 리턴타입을 그대로 body에 담아 응답을 하기 위해서는 `@ResponseBody`를 활용할 수 있습니다.

### 학습 테스트

- 테스트 메서드: `cholog.ResponseJsonTest.responseJson`
- 수행 방법
    - `cholog.MemberController.json` 메서드를 작성하여 학습 테스트를 성공시키세요.
    - `/json` 요청 시 `{"name": "brown", "age": 20}` 응답할 수 있도록 설정하세요.

<span style="color: green">   
`/json` 요청 시 : `@GetMapping("/json")`

`{"name": "brown", "age": 20}` 응답 

- `return new Person("brown", 20);`  : 객체 필요
- `@ResponseBody` : body를 응답
</span>

### 참고자료

- [Spring - @ResponseBody](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/responsebody.html#page-title)
- [Spring - Return Values > Other return values](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-methods/return-types.html)

# 코드
<https://github.com/KimGyeongLock/spring-learning-test/tree/roki/spring-mvc-1/spring-mvc-1/initial>
