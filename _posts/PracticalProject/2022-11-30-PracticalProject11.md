---
layout: single
title: DI
toc: true
toc_sticky: true
categories: Practical
published: true
---

# Spring CRUD 개발
## Spring MVC framework review
1. 웹 브라우저 -> Dispatcher Servlet (request “/“(root directory))
    * Dispatcher Servlet: 모든 request를 처리하는데 가장 중심
    * servlet-context.xml: dispatcher servlet에 관련된 설정 내용 포함
2. request에 해당되는 Handler Mapping을 통해서 root의 url의 해당되는 페이지 서비스를 어떤 Controller가 담당하는 지 찾아냄

3. Controller에서 페이지를 만들어내기 위해 필요한 모델을 구성 
    * HomeController.java: root라는 특정한 jsp페이지를 명시하지 않고 URL의 root라고 되어 있는 부분을 처리할 수 있도록 기본적으로 세팅
4. Model: 어떤 모델에 어떤 data set가 처리되어야 하는지 Controller에 전송
    * ???VO.java: database에 저장되어 있는 특정한 테이블의 레코드 타입을 그대로 하나의 객체로 담고 있음
    * ???Dao.java: 담겨진 객체들을 어떤 식으로 access 할 것인가라는 부분
        * 필요에 따라서 DB를 액세스 하는 부분 존재
        * 쿼리를 던져서 가져오는 레코드 set이나 쿼리의 결과물 
6. 해당하는 모델을 완성해서 Dispatcher Servlet으로 전송
7. Dispatcher Servlet은 View를 준비
8. View Resolver를 통해 request에서 제시했던 root라는 url의 해당되는 뷰가 무엇인지 알아냄 (root: home.jsp)
9. Dispatcher Servlet에서 home.jsp를 구동해서 나온 결과물을 response로 클라이언트에게 전달


## 프로젝트 폴더 구조
* src/main/java: class 폴더
    * .java 파일들의 모임
    * 패키지 이름으로 구분해서 기능/용도별로 구조화
* src/main/resources: 리소스 보관용
    * DB 연결, 의존성 주입을 위한 xml 파일 등
* Maven Dependencies
    * Maven에서 관리하는 라이브러리 폴더(pom.xml 내용 참조)
* src/main/webapp/WEB-INF/views
    * 웹 사이트 파일들의 루트(/) (.jsp, .html 등)

----------

# 의존성 주입(DI)
## DI(Dependency Injection)
* 의존성 주입
    * 하나의 객체(B 객체)가 다른 객체(A객체)에게 의존성을 제공하는 기술
    * 객체간의 의존성, 결합도는 줄이고, 코드의 재활용성은 높이게 됨
    * 필요한 객체를 직접 생성하지 않고 외부에서 생성하여 주입되어 사용함
        * Spring framework에 의해 동적으로 주입

## Spring IoC(Inversion of Control)
* Spring IoC(Inversion of Control)
    * 객체(Bean)의 생성, 의존관계를 Spring컨테이너가 자동 관리
    * 객체간 결합도 최소화되어 유지보수 향상
    * 방법
        * 의존성 검색(Dependency Lookup)
            * 컨테이너가 생성한 객체를 클라이언트가 검색하여 사용
        * 의존성 주입(Dependency Injection)
            * 컨테이너가 의존관계를 통해 필요한 곳에 자동 주입

## Spring DI(Dependency Injection)
* 의존성 주입 방법
    * Bean 생성
        * XML 설정파일
        * Annotation 사용
    * 컨테이너가 객체간의 의존관계에 따라 필요한 객체를 주입
        * Constructor Injection
        * Setter method Injection
        * Field Injection
* EX) XML 설정
1. Interface 생성: 결합도를 낮추기 위함<br/>
   * Coffee Interface
2. Interface 구현한 클래스 생성<br/>
   * Americano class
   * CafeLatte class
3. 의존 객체를 사용하는 클래스 생성<br/>
   * MyCafe class
4. XML에 Bean 등록<br/>
   * Americano, CafeLatter, MyCafe
5. XML에 객체간 의존관계 설정<br/>
   * Constructor
   * Setter Method
6. Test<br/>

----------

# Annotation
* 개념
    * 자바 소스 코드에 @Annotation의 형태로 특별한 기능 표현
    * Spring에 DI(Bean wiring), Bean 등록, 탐색 등에 사용
    * 클래스, 메소드, 필드 선언에서 @Annotation 사용
    * 컴파일 과정에서 어노테이션 정보로 코드 자동 생성
* 사용목적
    * 어플리케이션이 커질수록 XML 설정 작업이 복잡해짐
    * Java source 필요한 곳에 어노테이션을 사용하여 코드의 가독성 향상
    * 사용법이 간단함
* Annotation 설정
    * Spring 설정 파일에 context namespace 설정
    * Component Scan 설정 : @Annotation을 이용하여 bean 자동 생성
    * 소스에 Annotation 설정
* Bean 등록 Annotation
    * @Controller: Presentation layer
        * 웹 요청과 응답을 처리하는 클래스
    * @Service: Service layer
        * 비즈니스 로직을 가지는 클래스
    * @Repository: Persistence layer
        * 파일이나 데이터베이스를 처리하는 클래스(DAO)
    * @Component
        * Spring이 Bean으로 등록하는 가장 기본적인 annotation
        * 기본 생성자 반드시 필요
* DI Annotation
    * @Autowired
        * 생성자, 멤버함수, 멤버변수 위에 설정
        * Spring container는 Bean으로 생성된 객체 중에 같은 타입의 객체를 찾아 멤버변수에 자동 주입
        * @Inject로 대체 가능

----------

# Spring web service 구조
1. web.xml 파일을 읽고, 그 안에 있는 spring 빈 설정 파일들을 읽어들이면서 빈 생성, veiw resolver 여러가지 설정
2. client로부터 요청이 들어오면 DispatcherServlet이 동작
3. 요청이 들어온 URL을 실행할 수 있는 Controller를 찾아서 Controller에게 실행권을 줌
4. Controller가 해당하는 함수를 동작하면서 그 안에서 실제 서비스 쪽에 프로그램을 돌림
5. ServiceImpl 실행
6. 내부적으로 DAO 실행, 데이터베이스에 실제 작업, 데이터를 가져옴
7. 가져온 내용을 ServiceImpl -> Controller로 전송
8. Controller가 현재 가지고 있는 데이타 모델들을 가지고 데이터를 어디에 보여줄지 뷰 페이지 정보를 DispatchServlet에 전송(Model and View)
9. 정보를 View Page에 넘기게 됨
10. HTML page 생성 -> response


* 프로젝트 생성 방법
1. application-context.xml (Bean xml 설정작업)
2. VO (데이터베이스에 있는 테이블의 데이터를 가져오기 위해서 객체 클래스)
3. DAO (value obejct와 데이터베이스의 연결해서 실제 CRUD 메소드 즉 쿼리문을 실행할 수 기능을 가진 함수)
4. Service interface
5. ServiceImpl (데이터 가공)
6. Controller (Request mapping url, url요청이 왔을 때 실행해야되는 함수들을 생성)
7. Veiw(jsp page)
