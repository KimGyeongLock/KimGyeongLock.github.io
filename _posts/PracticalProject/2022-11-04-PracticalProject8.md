---
layout: single
title: JSP
toc: true
toc_sticky: true
categories: Practical
published: true
---

# Web Server & Client

* 웹브라우저 or 웹크롤러(Clients) -> 웹 서버(or WAS) : **request**
* 웹 서버(or WAS) -> 웹브라우저 or 웹크롤러 : **response**
    * response는 html 표준을 따라서 response를 보내줌
    * request 내용이 html이면 파일 그대로 보내줘도 됨
    * html은 정적 (static) 정적인 웹사이트를 구동하는 사이트는 많지 않음
    * 보통은 database에 들어있는 여러 내용들을 바탕으로 해서 program이 들어가는 방식으로 개발 (Web Service = Web application)
* Server Platform
    * JSP (Java Server Pages) 
    * Tomcat(웹서버)
    * Spring(서버 Framework)
    * MySQL(Database)

--------------

# JSP Web development Platform
* JSP Web service flow
    * Clients -> Web Server (Request(???**.jsp**))
        * 1. JSP 파일을 해독하여 java 코드부분을 확인
        * 2. java compile (class 생성)
        * 3. class 로딩 및 실행
        * 4. 결과를 HTML 페이지에 결합
        * 5. 클라이언트로 전송
    * Web Server -> Clients (Response(HTML page))
    * 위 과정을 수행하기 위해서는 **서버 환경 구축** 필요!
        * **Java 개발도구**
            * OpenJDK
            * Oracle Java JDK
        * **웹 애플리케이션 서버(WAS)**
            * Tomcat
                * ASF(Apache Software Foundation)에서 개발한 웹 어플리케이션 서버(WAS)
                * jsp로 개발되는 웹 사이트 구동 엔진
        * **통합개발환경(IDE)**
            * STS(Spring Tool Suite)
            * Eclipse
            * IntelliJ

--------------

# JSP Scripting elements
* jsp안에 java code를 집어넣는 방법
1. script let tag
	```
	<% java source code %>
	```
	* 변수만 선언 가능
	* 메소드 선언X Call은 가능
	* 코딩이 조금 들어가야 한다
2. expression tag
	```
	<%= statement %>
	```
	* 간단하게 출력
3. declaration tag
	```
	<%! field or method declaration %>
	```
	* 변수, 메소드 선언 가능

--------------

# JSP Implicit Objects
* 내가 따로 선언해서 object로 instantiation 안해도 jsp page가 서버로부터 실행이 될 때 자동적으로 만들어지는 객체
* Tomcat에 web container에 자동으로 만들어짐 필요할 때마다

|객체명|타입|설명|
|:---:|:---:|:---:|
|**out**|JspWriter|JSP페이지에서 데이터 출력에 사용하는 스트림 객체|
|**request**|HttpServletRequest|웹 브라우저로부터 전달된 request 정보를 저장하는 객체|
|**response**|HttpServletResponse|웹 브라우저로 전송할 response 정보를 저장하기 위한 객체|
|**session**|HttpSession|웹 브라우저와 웹 서버간 세션 정보(로그인, 장바구니..)를 저장하는 객체|
|application|ServletContext|웹 애플리케이션 범위의 context 정보를 저장하는 객체|
|pageContext|PageContext|JSP 페이지 범위의 속성 등의 정보를 저장하는 객체|
|page|Object|JSP 페이지 자신을 가리키는 객체|
|config|ServletConfig|JSP 페이지에 대한 초기 설정 정보를 저장하는 객체|
|exception|Throwable|JSP 페이지에서 예외 처리에 사용되는 객체|

-----------

# Form 데이터 처리 구조(localhost(PC))
* PC안에 Client와 Server가 공존
* Client: Browser
* Server: Tomcat
    * Web server + WAS
    * form.html -> form_ok.jsp <-> DBMS

-----------

# Deployment(Heroku)

## Deploy a web application
* Local PC (Web browser + Web Server)
    * 개발과 실행을 동시에 함 (Tomcat)
* local pc에서 서비스를 실행한다해서 전체 인터넷에서 서비스가 되지 않음
    * 반드시 로컬 서버에서 개발한 서비스들을 패키지로 만들어서 웹서버로 쓸 수 있는
    * WAS 서버에 직접 올려야지만 url을 통해서 서비스를 제공받을 수 있다.
    * WAS 서버 = heroku
    * heroku를 사용하게 된다면 heroku에서 데이터베이스 서버에 접속해서 필요한 DB 작업을 하게끔 진행

## Web Service 개발 및 배포
* Project 생성 및 기획, 개발, 테스트
    * Local PC
* 협업 진행: VCS 사용 (Git, Github)
* Deploy
    * Tomcat hosting 신청
    * 클라우드 컴퓨팅 서비스 신청(PaaS, Platform as a Service)
        * Heroku(PaaS): 애플리케이션을 개발, 실행, 및 관리
