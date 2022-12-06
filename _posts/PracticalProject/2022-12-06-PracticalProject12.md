---
layout: single
title: MyBatis, Spring Interceptor
toc: true
toc_sticky: true
categories: Practical
published: true
---

# MyBatis framework
* RDB(Relational Database) 프로그래밍을 쉽게 해주는 Java Persistence framework
* JDBC(Java Database Connectivity)를 편하게 사용할 수 있음
* SQL문과 자바 객체 간의 Mapping 기능 제공
* 간단한 코드로 DB 연동 처리 가능
* **SQL문은 자바코드에서 완전히 분리하여 XML 파일에 별도 관리**
* Spring과 연동하여 자동화 처리
* 유지보수성 향상(동적 SQL 사용)
* 아파치 소프트웨어 재단에 개발한 iBATIS는 2010년에 구글코드로 이전하면서 MyBatis로 이름 변경

-------------

# Spring web project
Controller -> Service -> DAO -> MyBatis -> Database<br/>
Controller <- Service <- DAO <- MyBatis <-

-------------

# MyBatis-Spring 연동

* **SqlSessionFactoryBean 클래스**
    * 설정파일에 빈으로 등록하여 SqlSessionFactory 객체 생성
    * dataSource 를 사용하여 데이터베이스에 연결
    * MyBatis 설정파일 위치 설정
    * Mapper 파일 위치 설정
* **SqlSessionTemplate 클래스**
    * public Object selectOne(String stmt, Object param)
    * public List selectList(String stmt, Object param)
    * public int insert(String stmt, Object param)
    * public int update(String stmt, Object param)
    * public int delete(String stmt, Object param)

-------------

# MyBatis 구성
* **MyBatis configuration file(xml)** : MyBatis가 JDBC 사용을 위해 필요한 설정
    * \<typeAlias\>
    * \<environment\> : DB 접속에 대한 설정
    * \<mapper\> : Mapper 파일 위치 설정
* **Mapper files(xml)** : SQL문 관련 설정
    * SQL문, parameter, result, resultMap(ResultSet)
    * Insert, delete, update, select
    * \<sql\> 태그 사용

-------------  
  
# MyBatis 설정파일
* Connection pool 제공
    * 미리 데이터베이스 connection을 생성
* 다수 데이터베이스 연결 정보 설정 및 선택 가능
* VO(Value Object)에 alias 설정

## Mapper xml : parameter, result type
* 여러 데이터 사용을 위해 VO 객체 사용
* 자바 클래스 전체 경로 포함
* (패키지+)클래스 이름이 긴 경우 \<typeAlias\>를 이용하여 별칭으로 사용

## Mapper xml : CDATA Section
* SQL문에 특수기호 \<,\> 등의 기호를 사용할 때 xml에 의해서 연산자로 처리되는 것을 막기 위함
* CDATA Section 내의 구분은 XML parser가 해석하지 않음

-------------
  
로그인 기능 구현

# Fileter Interceptor, AOP
* 프로그램 내에서 자주 사용되느 공통 기능을 따로 구현하여 처리하는 방법
* **Filter** : DispatcherServldet이 실행되기 전과 후 수행되는 기능을 처리
    * Encoding, XSS방어
* **Interceptor** : DispatcherServlet이 Controller를 호출하기 전과 수행되는 기능을 처리
    * http 프로토콜에 존재하는 정보를 활용가능(로그인 여부 확인)
    * dispatcher servlet과 Controller 사이에서 공통된 기능을 넣고자 할 때 사용
* **AOP**(Aspect Object Programming)
    * Controller 처리 이후 비즈니스 로직에서 실행
    * 로깅, 트랜잭션, 에러 처리
* 차이점: 실행되는 위치가 다름<

Request -> Filter -> Dispatcher Servlet -> Interceptor -> Controller -> AOP -> Service<br/>
Request <- Filter <- Dispatcher Servlet <- Interceptor <- Controller <- AOP <- 

-------------  

# HandlerInterceptor
* 특정 URI 호출을 가로채는 역할
* 기존 컨트롤러 변경없이 사전이나 사후 제어가 가능
* 여러 URL에 적용하는 기능을 구현할 때 사용
* 로그인 여부 체크

-------------  
  
# Interceptor 생성
* HandlerInterceptorAdapter를 상속받는 Interceptor 생성
    * **boolean preHandle(request, response, handler)**
        * 전처리기, 클라이언트에서 요청 후 Controller 호출 전에 실행
        * Dispatcher servlet -> controller
    * **void postHandle(request, response, handler)**
        * 후처리기, Controller 호출 후 실행됨
        * controller -> Dispatcher servlet
    * **void afterCompletion(request, response, handler, modelAndView)**
        * Controller처리 및 화면처리 후 실행
        * view -> DispatcherServlet
