---
layout: single
title: Database
toc: true
toc_sticky: true
categories: Practical
published: true
---

# File vs Database

* 파일 시스템의 문제점
    * 응용 프로그램과 데이터(파일)간에 상호 의존성이 존재
    * 프로그램과 파일은 보통 1:1로 대응
    * 한 시스템 내에서 데이터가 중복 저장되어 관리
    * 일관성 어려움 / 보안성 / 중복 저장으로 인한 경제성 저하 / 다중 사용자 사용 어려움(효율성)
* 데이터베이스 특징
    * 실시간 접근성 (Real-time accessibility)
        * 다수 사용자의 요청에 대해 몇 초 내 응답
    * 지속적인 변화 (Continuous evolution)
        * 최신의 데이터가 정확하게 저장
    * 동시 공유 (Concurrent sharing)
        * 동일한 데이터를 서로 다른 목적으로 사용
    * 내용에 의한 참조 (Content Reference)
        * 값에 의한 참조 

-------------

# Database

* 데이터베이스(Database)
    * 구조화된 정보, 데이터의 조직화된 모음
* 데이터베이스 관리 시스템(DBMS, Database Management System)
    * 수많은 데이터를 편리하게 저장하고, 효율적으로 관리, 검색할 수 있는 데이터베이스 관리 시스템
* 데이터베이스 유형
    * 관계형데이터베이스, 객체지향 DB, 분산DB, NoSQL 데이터베이스 등
* RDBMS (Relational DBMS)
    * 관계형 데이터베이스 관리 시스템
    * 데이터베이스 내의 테이블은 서로 연관되어 데이터를 저장, 구성, 관리
    * 데이터를 관리하기 위해 SQL (Structured Query Langauge) 사용
    * MySQL, MariaDB, PostgreSQL, Oracle, Informix(IBM), SQL Server(MS) 등

-------------

# SQL

* SQL(Structured Query Language)
    * 모든 관계형 데이터베이스(RDBMS)에 사용
    * 데이터를 정의, 조작, 쿼리, 엑세스를 제공하기 위한 프로그래밍 언어
    * CRUD, Schema 생성, 수정, 조회 등 관리를 위해 설계된 프로그래밍 언어
* SQL 종류
    * DDL(Data Definition Language)
        * 테이블, 인덱스, 제약조건 등 정의
        * create, alter, drop, rename 문
    * DML(Data Manipulation Language)
        * 데이터 추가, 수정, 삭제, 조회
        * insert, update, delete, select 문
    * DCL(Data Control Language)
        * 사용자 권한, 트랜잭션 등 처리
        * grant, revoke, truncate 문

-------------

# 데이터베이스 구조

* 데이터베이스 설치
    * 관계형 데이터베이스 종류 선택
    * 데이터베이스 (DBMS) 설치
    * 샘플 데이터베이스 다운로드
    * 데이터베이스 연결 및 명령어 실행
* 데이터베이스 관리 어플리케이션(클라이언트)
    * 데이터베이스 종류마다 다양한 프로그램을 가짐
    * 데이터베이스 연결
    * SQL문 실행

-------------

# MySQL(MariaDB)

* RDBMS (관계형 데이터베이스 관리시스템)
* 가장 많이 사용되는 오픈소스 관계형 데이터베이스 관리 시스템
* CLI 명령어로 관리 - GUI 프로그램 사용
    * MySQL Workbench, DBeaver
* 오라클(Oracle)이 인수 후 관리 및 지원
* 다양한 프로그래밍 언어로 API 지원
    * Java, C++, C#, python, ruby 등

-------------

# DBeaver 

* DB관리를 위한 GUI tool
* Database 클라이언트 도구
* 데이터베이스 접속 후 SQL 문 실행

-------------

# 데이터베이스 구성방법

1. 데이터베이스 생성
2. 데이터베이스 스키마(Tables)
3. 테이블은 여러개의 필드로 구성
4. 생성된 테이블을 이용하여 CRUD를 위한 SQL문 작성

-------------

# SQL문 - 테이블 생성
* DDL(Data Definition Language) 이용
    * 필드 타입: Database별로 제공
        * 정수형: int
        * 실수형: float, double
        * 문자형: char(n), varchar(n)
        * 날짜형: date, time, date time, timestamp
```
create table person (
	PersonID int not null auto_increment,
	LastName not null varchar(50),
	FirstName varchar(50),
	Address varchar(1000),
	City varchar(200),
	Regdate timestamp default current_timestamp,
	primary key(PersonID)
);
```
> not null: null을 허용하지 않음<br/>
> auto increment: 1씩 증가<br/>
> current_timestamp: 현재 시간을 default값으로 설정

-------------

# SQL문 - Read(List)
* DMS(Data Manipulation Language) 이용
* SELECT column1, column2, …
    * 원하는 필드의 이름을 조회
* FROM table_name
    * 가져올 테이블 이름
* WHERE column1 = ‘value1’
    * 조건 추가
* WHERE column1 = ‘value1’ and …
    * 여러개 조건 추가
* WHERE column1 like ‘value1%’ or …
    * 글자가 들어가 있는 조건
* ORDER BY column1, column2 desc
    * 정렬
* Limit 0, 5
    * 0~5번까지만 가져오기

-------------

# SQL문 - Insert / Update / Delete
 
* DML(Data Manipulation Language) 이용
* 데이터 추가
  ```
  INSERT INT0 tablename (column1, column2, column3, …) VALUES (value1, value2, value3, …);
  ```
* 데이터 수정
  ```
  UPDATE tablename
  SET column1 = value1, column2 = value2, …
  WHERE condition;
  ```
* 데이터 삭제
  ```
  DELETE FROM tablename WHERE condition;
  ```
