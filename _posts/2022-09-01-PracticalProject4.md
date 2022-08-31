---
layout: single
title: Java CRUD
toc: true
toc_sticky: true
categories: Practical
published: true
---

# 수업내용
* **객체지향프로그래밍**: 자바의 특징
* **Maven** - 프로젝트 관리도구(Build tool)
* Java를 이용한 CRUD
* 파일 입출력 (Save and Load)
* **데이터베이스** : **SQLite**
* 기본 SQL (insert, update, delete, select 문)
* **JDBC**로 데이터베이스를 이용한 데이터 관리
* **MyBatis framework** 사용한 데이터 관리

-----------

# 프로젝트 구성
객체지향프로그램이기 때문<br/>
**Class**와 **Interface** 중점<br/>
* **Word class**: <span style="color: blue">**데이터클래스**</span>
    * 영어단어 데이터
    * 데이터를 다루기 위해서 만드는 클래스
    * 기본적으로 데이터가 가지고 있는 데이터 구조의 변수 내포
        * **private**으로 하게 되면은 같은 클래스 내부에서만 접근이 가능하고 외부에서는 접근이 불가능
        * 외부에서 변경할 수 있도록 **getter**와 **setter**를 추가
    * 데이터를 사용하기 위해서 **getter**와 **setter**가 필요
    * 데이터를 초기화하기 위해서 생성자인 **constructor**가 필요
* **ICRUD interface**: <span style="color: blue">**CRUD를 위한 interface**</span>
    * CRUD의 기본적인 함수의 이름을 미리 템플릿으로 정하기 위해서 CRUD를 위한 interface 생성
* **WordCRUD class**: <span style="color: blue">**ICRUD interface 구현체**</span>
    * ICRUD를 실제 구현한 단어를 다루는 CRUD 구현체
    * 데이터 클래스로 Word class를 사용
    
<br/>
<span style="color: red">구현체는 하나인데 굳이 interface를 만들 필요가 있을까?</span><br/>
➔ 이 프로그램은 단어를 관리하는 프로그램이지만 다른 기능들을 넣을 수 있을 때를 대비해서 확장 가능성을 생각하여 interface로 구현<br/>
<br/>

* **WordManager class**: <span style="color: blue">**wordCRUD를 사용한 실제 관리**</span>
    * WordCRUD라는 클래스를 이용해서 실제 전체 프로그램 Managing
    * 사용자에게 보여주는 UI 담당
* **Main class**: <span style="color: blue">**static main 함수, starter class**</span>
    * 자바 프로젝트를 처음으로 구동하기 위해서 main이라는 함수가 실제 실행이 되는데, main 함수를 가지고 있는 클래스
    * Main 클래스에서 WordManager를 호출함으로써 프로그램이 시작

-----------

# CRUD 작성 및 테스트
* WordManager class
    * selectMenu 함수 
* WordCRUD class
    * Create : Word 추가
    * Read : Word 조회
* Word class
    * toString() : overriding
<br/>
<br/>

* 데이터 조회
    * WordManager class
        * 모든 단어 보기 메뉴 처리
    * WordCRUD class
        * listAll() 함수 생성
    * Word class
        * toString() : overriding
