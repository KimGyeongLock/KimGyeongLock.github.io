---
layout: single
title: Spring Framework
toc: true
toc_sticky: true
categories: Practical
published: true
---


# Web Architecture
* **Controller**
    * 사용자 요청 처리
    * 화면의 로직 처리
* **Model** 
    * 알고리즘, DB와 상호작용(CRUD)
    * sql문 실행, 결과 데이터 처리
* **View**
    * 사용자에게 보여줄 UI(User Interface)
* **JSP Model1 Architecture**
    * 90~2000년 초까지 웹 개발 아키텍쳐
    * JSP와 Java Bean으로 구성
        * JSP = Controller + View
        * Java Bean = Model
    * 로직(Controller)와 화면(View)가 통합되어 유지보수 어려움
* **JSP Model2 Architecture (MVC Architecture)**
    * Model, View, Controller 의 분리
    * 대규모 MVC 어플리케이션의 문제로 다양한 패턴이 생김(MVVM, MVP…)

------------

# JSP Model1 Architecture
* Model1 구성
    * JSP page
        * Controller
        * View
    * Java Bean
        * Model
          
   |구성|파일|특징|
   |:---:|:---:|:---:|
   |Controller|Servlet Class|입력정보 추출<br/>```<br/>String id = request.getParameter(“userid”)<br/>```|
   |View|JSP Page|UI(User Interface)담당|
   |Model|VO, DAO Class|DB 연동|

* 동작 원리
1. 사용자가 웹 브라우저(Web clients)를 통해서 hello.jsp 파일 요청
2. Web Server가 요청을 받아서 hello.jsp 파일에 대한 요청을 Servlet(JSP) Container로 전송 
      * **Servlet(JSP) Container**
        * Servlet 변환 (helloServlet.java)
        * class 파일 생성 (helloServlet.class)
        * 메모리에서 실행<br/>
3. 해당하는 JSP(Controller + View)파일과 Java Bean(Model) 실행
4. dao를 이용해서 데이터 베이스에 접속
5. 데이터베이스에서 조회한 데이터를 가지고 와서 Controller로 전송, 가져온 데이터를 View를 통해서 html로 만듦
6. 만든 결과물을 Web Server로 전달
7. Web Server가 요청한 곳에다 Response

-------------

# JSP Model2(MVC) Architecture
* Model2 구성

|구성|파일|특징|개발|
|:---:|:---:|:---:|
|Model|Service class<br/>Java Beans|- DB 연동<br/>- 데이터 가공|자바개발자|
|View|JSP Page|- UI(User Interface)담당<br/>- Request객체나 session 객체로 화면 출력|웹 디자이너|
|Controller|Servlet Class|- 입력정보 추출<br/>- Model class의 DB 연동 함수 호출<br/>- 페이지 이동|자바 개발자<br/>MVC framework|

* 동작 원리
   1. 사용자가 웹 브라우저(Web clients)를 통해서 hello.jsp 파일 요청
   2. Web Server가 요청을 받아서 hello.jsp라는 파일에 대한 요청을 Web Container로 전송
   3. hello.jsp에 해당하는 Servlet(Controller)이 가장 먼저 응답
       * Controller - class file
   4. 이에 필요한 Java Beans을 불러서 데이터를 가져옴
   5. 그 데이터를 이용해서 어떤 뷰와 연결해야될지 서로 작동
       * View - JSP page
   6. Controller가 View와 Model을 합치는 작업
   7. 웹페이지가 생성이 완료되면 Web Server로 전송
   8. Web Server가 요청한 곳에다 Response

--------------

# Spring framework
* 자바를 위한 가장 인기있는 애플리케이션 개발 프레임워크
* Open Source Java Platform
* 쉬운 테스트 및 재사용 가능한 코드 작성
* Java Application 개발 및 Web Application 확장 가능
* Spring Container + Bean 으로 구성
* 약 20개의 모듈로 구성된 기능
* 전자정부프레임워크를 구성하는 프레임워크

## Spring framework 장점
* **POJO Based**
    * POJO(Plain Old Java Object)를 사용한 엔터프라이즈급 애플리케이션 개발
* **Modular**
    * 모듈화가 되어 있어 패키지와 클래스 수가 많아도 필요한 것만 코딩
* **Web MVC**
    * 잘 설계된 웹 MVC framework
* **JDBC, Hibernate, JPA 등 기술을 위한 다양한 템플릿 제공**
    * JdbcTemplate을 사용하면 JDBC 연결 생성, 예외 처리, transaction commit, 연결 닫기 등이 필요없으며 쿼리 실행부분 코드만 작성하면 됨
* **LightWeight**
    * 메모리와 CPU 리소스가 제한된 컴퓨터에서 응용 프로그램을 개발, 배포에 유용
* **Loose Coupling**
    * DI(Dependency Injection)으로 인해 느슨한 결합 지원
* **Easy to test**
    * 종속성 주입(DI)를 사용하여 쉬운 테스트 가능
* **Transaction management**
    * Spring은 축소와 확장할 수 있는 일관된 transaction 관리 인터페이스 제공

--------------

# IoC(Inversion of Control)
* 제어의 역전
* 객체의 생성부터 소멸까지 생명주기를 개발자가 아니라 컨테이너가 대신 관리
* IoC Container = Bean Container + 의존 객체 자동 주입(DI)
* Spring framework에서 IoC Container 사용

--------------

# Spring Container
* Spring framework 핵심
* Spring framework의 초기화 역할 담당
* 컨테이너의 역할은 객체 생성, 연결, 구성, 전체 수명주기 관리
* 컨테이너는 POJO 클래스와 메타 데이터 사용하여 구성, 애플리케이션 실행


