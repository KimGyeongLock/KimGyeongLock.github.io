---
layout: single
title: Spring1 (프로젝트 생성)
toc: true
toc_sticky: true
categories: javaSpring
published: true
---

## \#1 
<img width="802" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/1ba96ca8-29ab-4cf1-8f9d-0adfba9fe759">

- **Spring Initializr**
create **Spring Boot** applications using the Spring Initializr service
- Type : **Gradle** - Groovy
- JDK : 17 (오류가 안났음)

> **Spring Boot**
: 세 가지 핵심 기능을 통해 Spring Framework를 사용하여 더 빠르고 쉽게 웹 애플리케이션과 마이크로서비스를 개발하도록 돕는 툴.
1. 자동 구성
2. 구성에 대한 독선적 접근 방식
3. 독립형 애플리케이션을 만드는 능력    
  [https://www.ibm.com/kr-ko/topics/java-spring-boot](https://www.ibm.com/kr-ko/topics/java-spring-boot)
> 

> **Gradle vs Maven** (Build Tool)         
[https://medium.com/@samuelcatalano/maven-vs-gradle-key-differences-81d366bf45d6](https://medium.com/@samuelcatalano/maven-vs-gradle-key-differences-81d366bf45d6)
> 
> 
![Untitled 1](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/e18fdfb9-3ea5-4c00-923a-e8389254bda2)
> 

## \#2 
<img width="798" alt="Untitled 2" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/a0232c7c-622f-4008-99e4-9407705ff398">

- **Lombok**
: Java annotation library which helps to reduce boilerplate code.
    - 어노테이션 기반으로 코드를 자동완성 해주는 라이브러리이다. Lombok을 이용하면 Getter, Setter, Equlas, ToString 등과 다양한 방면의 코드를 자동완성 시킬 수 있다.
- **Spring Web**
: Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.
    - Spring Web을 이용하면 웹을 더 편리하고 빠르게 만들 수 있으며 다양한 기능과 도구를 제공하여 개발자의 부담을 덜어주는 도구


## \#3 
<img width="496" alt="Untitled 3" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/235850ab-5e26-4174-b662-b9043bd23794">

- Reload All Gradle Projects

<img width="1403" alt="Untitled 4" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/60e525bb-ab08-4038-b8a5-70c9c4d91638">

- 성공


## 에러

```sql
Execution failed for task ':compileJava'.
> error: invalid source release: **22**

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
> Get more help at https://help.gradle.org.
BUILD FAILED in 3s
1 actionable task: 1 executed
```

- build.gradle
    - version에 맞게 수정
    
    ```sql
    java {
        sourceCompatibility = **'17'**
    }
    ```
