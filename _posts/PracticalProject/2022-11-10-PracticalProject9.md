---
layout: single
title: JSP 문법
toc: true
toc_sticky: true
categories: Practical
published: true
---

# JSP Directives
* JSP 페이지를 servlet 클래스로 변환할 때 필요한 여러 정보들을 기술하기 위해 사용
  ```
  <%@ directive attribute = “value”%>
  ```
  >  directive: 지시어<br/>
  >  attribute: 속성 이름
* **page directive**
    * jsp 전체 페이지에 적용되는 정보 기술
* **include directive**
    * 다른 jsp or html 페이지를 불러와 현 페이지의 일부로 추가
* **taglib directive**
    * JSP 문법 중 Action or JSTL 등 사용자 정의 태그 사용할 때 필요
      ```
      <%@taglib prefix=“c” uri=“http://java.sun.com/jsp/jstl/core” %>
      ```
      > prefix: 현재 페이지에서 tag library를 나타내는 이름<br/>
      > uri:  tag library가 있는 주소

-----------

# page directive
* contentType 속성
  ```
  <%@page contentType=“text/html; charset=euc-kr” %>
  ```
  > charset = eur-kr or UTF-8
* import 속성
  ```
  <%@page import=“java.util.ArrayList” %> // 하나의 클래스
  <%@page import=“java.util.* %> // 패키지 내 모든 클래스
  <%@page import=“java.util.*, java.io.*” %> // 여러 패키지내 클래스
  <%@page contentType=“text/html; charset=euc-kr” import=“java.util.*” %>
  ```
* buffer, autoFlush, isThreadSafe, session, errorPage, isErrorPage, isELIgnored, pageEncoding …

-----------

# include directive
```
<%@include file=“top.jsp” %>
Hello World~
<%@include file=“footer.jsp” %>
```
> top.jsp를 미리 만들어놓고 include 지시어를 이용해서 가져오게 되면 한 페이지 처럼 보임

-----------

# JSP Action Tags
* 페이지 간의 flow 제어, 자바 bin이라는 자바 클래스를 사용하는데 많이 사용
* **jsp:forward**
    * 다른 페이지나 리소스로 이동할 때 사용
      ```
      <jsp:forward page=“list.jsp” />
      ```
* **jsp:param**
    * 파라미터를 설정할 때 사용
      ```
      <jsp:forward page=“list.jsp”>
      <jsp:param name=“name” value=“ok!!” />
      </jsp:forward>
      ```
      > 현재폴더/list.jsp?name=ok
* **jsp:include**
    * 다른 페이지나 리소스를 포함하여 사용
      ```
      <jsp:include page=“top.jsp” />
      ```
    * include 지시어: 
        * 원래 페이지 안으로 include 지시어로 만들어놓은 top.jsp 페이지 소스가 그대로 복사
    * jsp:include
        * 제어권이 top.jsp로 갔다가 다시 list.jsp로 오게됨
* **jsp:useBean**
    * 정보를 표현하기 위한 목적으로 자바 클래스를 만들게 되는데 그 클래스를 가져와서 사용 (java class)
      ```
      <jsp:useBean id= “instanceName” scope= “page | request | session | application” 
                    class= “packageName.className” type= “packageName.className” 
                    beanName=“packageName.className | <%= expression >”
      </jsp:useBean>
      ```
    * Bean 생성 -> Bean 사용
* **jsp:setProperty**
    * useBean에 있는 멤버 변수에 setter를 이용해서 값을 세팅할 때 사용
      ```
      <jsp:setProperty name=“bean” property=“*” />
      <jsp:setProperty name=“bean” property=“username” />
      <jsp:setProperty name=“bean” property=“username” value=“Kumar” />
      ```
* **jsp:getProperty**
    * 해당하는 멤버 변수에 해당하는 값이 있을 때 가져오는 것 
        ```
        <jsp:getProperty name=“obj” property=“name” />
        ```
        
-----------
        
# Expression Language(EL) in JSP
* Java Bin의 프로퍼티와 값을 JSP 표현식을 사용하는 것보다 더 간단히 사용할 수 있는 기술
* Request, Session, Application에서 값을 꺼낼 때도 사용
* 변수를 가져올 때 영역을 지정하지 않으면 순차적으로 찾아옴
    * pageScope / requestScope / sessionScope / ApplicationScope
      ```
      ${requestScope.member.no}
      ${sessionScope.user}
      ${param.name}
      ```
    * EL Operator 제공
        * \[\], \(\), 산술연산, 관계연산, 조건연산, 조건(a? b:c), 논리연산(&&,\|\|), empty


