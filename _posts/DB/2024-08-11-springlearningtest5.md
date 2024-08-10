---
layout: single
title: "[Spring-JDBC-1] JdbcTemplate"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. JdbcTemplate

스프링은 **데이터베이스와의 연동**을 쉽게 도와주는 여러 가지 도구와 방식을 제공합니다.

**JDBC(Java Database Connectivity)**는 자바에서 데이터베이스에 접속할 수 있게 도와주는 API입니다.

JdbcTemplate은 이러한 JDBC를 좀 더 편리하게 사용할 수 있도록 스프링에서 제공하는 템플릿 클래스입니다.

이를 사용하면 데이터베이스 연동 코드를 좀 더 간결하고 안정적으로 작성할 수 있습니다.

JdbcTemplate은 스프링 JDBC의 핵심이며 다른 고수준의 기능들도 결국 내부에서는 이 JdbcTemplate을 활용합니다.

<br>

JdbcTemplate은 핵심 JDBC 작업 흐름(예: 문장 생성 및 실행)의 기본적인 업무를 수행하며, 애플리케이션 코드는 SQL을 제공하고 결과를 추출하는 역할을 담당합니다.

JdbcTemplate 클래스는 다음과 같은 기능을 제공합니다.

- SQL 쿼리 실행
- statements 및 저장된 procedure all 업데이트
- ResultSet 인스턴스를 반복하고 반환된 매개 변수 값의 추출을 수행
- JDBC 예외를 캡처하여 org.springframework.dao 패키지에 정의된 일반적이고 더 유용한 예외 계층으로 변환

# 2. Querying (SELECT)

JdbcTemplate을 이용하여 SELECT 쿼리를 실행하는 여러가지 방법을 제공합니다.

**queryForObject**, **query**, **queryForList**, **queryForRowSet**, **queryForMap** 등의 메서드를 이용하여 쿼리를 실행할 수 있습니다.

# 3. Querying for a Single Object

JdbcTemplate의 **queryForObject** 메서드를 이용하여 단일 객체를 조회할 수 있습니다.

## 3.1 Object with Count

queryForObject의 첫 번째 매개변수는 **쿼리문**이며, 두 번째 매개변수는 **조회 결과를 매핑할 클래스 타입**입니다.

```java
int rowCount = jdbcTemplate.queryForObject("select count(*) from customers", Integer.class);

```

### 학습 테스트

- 테스트 메서드: `cholog.QueryingDaoTest.count`
- 수행 방법
    - `cholog.QueryingDAO.count` 을 이용하여 학습 테스트를 성공시키세요.

<br>

`runtimeOnly 'com.h2database:h2'` 의존성은 H2 데이터베이스를 런타임에 사용하도록 설정

- H2는 Java 애플리케이션에서 흔히 사용하는 경량 임베디드 관계형 데이터베이스이다.
    - In-memory mode
    - Embedded mode
    - Server mode

`queryForObject` : 단일 객체를 반환할 때 사용

- 단일 객체 ⇒ 주로 결과가 **한 행**인 경우에 적합
- 여러 행을 반환해야 할 경우에는 `query` 메서드를 사용

## 3.2 Object with Parameter

queryForObject의 **세 번째 매개변수**를 이용하여 **쿼리문에 바인딩할 파라미터**를 전달할 수 있습니다.

```java

String lastName = jdbcTemplate.queryForObject("select last_name from customers where id = ?", String.class, id);

```

### 학습 테스트

- 테스트 메서드: `cholog.QueryingDaoTest.getLastName`
- 수행 방법
    - `cholog.QueryingDAO.getLastName` 을 이용하여 학습 테스트를 성공시키세요.

<br>

```java
public String getLastName(Long id) {
    //TODO :주어진 Id에 해당하는 customers의 lastName을 반환
String lastName = jdbcTemplate.queryForObject("select lastName from customers where id = ${id}", String.class);
    return lastName;
} 
```

> ${id} XX

## 3.3 Object with RowMapper

queryForObject의 두 번째 매개변수에 RowMapper를 전달하여 **조회 결과를 매핑**할 수 있습니다.

```java
Customer customer = jdbcTemplate.queryForObject(
        "select id, first_name, last_name from customers where id = ?",
        (resultSet, rowNum) -> {
            Customer customer = new Customer(
                    resultSet.getLong("id"),
                    resultSet.getString("first_name"),
                    resultSet.getString("last_name")
            );
            return customer;
        }, id);

```

### 학습 테스트

- 테스트 메서드: `cholog.QueryingDaoTest.findCustomerById`
- 수행 방법
    - `cholog.QueryingDAO.findCustomerById` 을 이용하여 학습 테스트를 성공시키세요.

<br>

`RowMapper` : **row 단위로 ResultSet의 row를 매핑하기 위해 JdbcTemplate에서 사용하는 인터페이스**
⇒ Row를 객체(`Customer`)에 매핑

```java
(resultSet, rowNum) -> {
    Customer customer1 = new Customer(
            resultSet.getLong("id"),
            resultSet.getString("first_name"),
            resultSet.getString("last_name")
    );
    return customer1;
}
```

# 4. Querying for a List

## 4.1 List with RowMapper

JdbcTemplate의 **query** 메서드를 이용하여 **여러 개의 객체를 조회**할 수 있습니다.

두 번째 매개변수에 **RowMapper**를 전달하여 조회 결과를 매핑할 수 있습니다.

```java
List<Customer> customers = jdbcTemplate.query(
        "select id, first_name, last_name from customers",
        (resultSet, rowNum) -> {
            Customer customer = new Customer(
                    resultSet.getLong("id"),
                    resultSet.getString("first_name"),
                    resultSet.getString("last_name")
            );
            return customer;
        });

```

queryForObject와 마찬가지로 의 세 번째 매개변수를 이용하여 쿼리문에 바인딩할 파라미터를 전달할 수 있습니다.

RowMapper의 경우 별도로 선언하여 사용할 수 있습니다.

```java
private final RowMapper<Customer> rowMapper = (resultSet, rowNum) -> {
    Customer customer = new Customer(
            resultSet.getLong("id"),
            resultSet.getString("first_name"),
            resultSet.getString("last_name"));
    return customer;
};

        ...

List<Customer> customers = jdbcTemplate.query("select id, first_name, last_name from customers where first_name = ?", rowMapper, firstName);

```

### 학습 테스트

- 테스트 메서드: `cholog.QueryingDaoTest.findAllCustomers`
- 수행 방법
    - `cholog.QueryingDAO.findAllCustomers` 을 이용하여 학습 테스트를 성공시키세요.

<br>

RowMapper를 별도로 선언

```java
RowMapper rowMapper = (resultSet, rowNum) -> {
    Customer customer = new Customer(
            resultSet.getLong("id"),
            resultSet.getString("first_name"),
            resultSet.getString("last_name")
    );
    return customer;
};
```

### queryForList

customers 내 모든 attributes가 무엇이 있는 지 궁금해서 h2 database를 열어봄.

하지만 in-memory 방식으로 작동하여 테스트가 끝나면 데이터가 없어지는 것을 알게됨,,

그래서 queryForList를 통해 test로 customers table을 출력해보았다.

```java
public void findAllCustomersWithAllAttributes() {
    String sql = "select * from customers";
    List<Map<String, Object>> customers = jdbcTemplate.queryForList(sql);

    for(Map<String, Object> customer : customers) {
        System.out.println(customer);
    }
}
```

<img width="329" alt="Untitled" src="https://github.com/user-attachments/assets/b60321a3-f550-4fa7-b4d2-6ccc23f1a538">

# 5. Updating (INSERT, UPDATE, and DELETE)

JdbcTemplate을 이용하여 INSERT, UPDATE, DELETE 쿼리를 실행하는 여러가지 방법을 제공합니다.

**update**, **batchUpdate**, **execute** 메서드를 이용하여 쿼리를 실행할 수 있습니다.

## 5.1 Update (INSERT)

JdbcTemplate의 update 메서드를 이용하여 INSERT, UPDATE, DELETE 쿼리를 실행할 수 있습니다.

```java

jdbcTemplate.update("insert into customers (first_name, last_name) values (?, ?)", customer.getFirstName(), customer.getLastName());

```

### 학습 테스트

- 테스트 메서드: `cholog.UpdatingDaoTest.insert`
- 수행 방법
    - `cholog.UpdatingDAO.insert` 을 이용하여 학습 테스트를 성공시키세요.

## 5.2 Update (DELETE)

```java

jdbcTemplate.update("delete from customers where id = ?", Long.valueOf(id));

```

### 학습 테스트

- 테스트 메서드: `cholog.UpdatingDaoTest.delete`
- 수행 방법
    - `cholog.UpdatingDAO.delete` 을 이용하여 학습 테스트를 성공시키세요.

`update`

- int 형태의 리턴을 하는데, **쿼리 실행 결과로 변경된 행의 개수**를 리턴

## 5.3 KeyHolder

JdbcTemplate을 사용하여 데이터베이스에 **새로운 정보를 추가**하고,

그 때 생성된 **primary key (여기서는 id)를 가져오기** 위해서 **KeyHolder**를 사용할 수 있습니다.

```java
KeyHolder keyHolder = new GeneratedKeyHolder();
jdbcTemplate.update(connection -> {
    PreparedStatement ps = connection.prepareStatement(
            "insert into customers (first_name, last_name) values (?, ?)",
            new String[]{"id"});
    ps.setString(1, customer.getFirstName());
    ps.setString(2, customer.getLastName());
    return ps;
}, keyHolder);

Long id = keyHolder.getKey().longValue();

```

### 학습 테스트

- 테스트 메서드: `cholog.UpdatingDaoTest.keyHolder`
- 수행 방법
    - `cholog.UpdatingDAO.insertWithKeyHolder` 을 이용하여 학습 테스트를 성공시키세요.

`GeneratedKeyHolder`

- 삽입된 레코드의 키 값을 추출하는 데 사용

`connection.prepareStatement(sql, new String[]{"id"})`

- `PreparedStatement`를 생성하면서, 삽입된 레코드의 자동 생성된 키(여기서는 `id`)를 반환하도록 지정

`PreparedStatement`가 데이터베이스에서 실행되면, 새로운 고객 레코드가 삽입되고, 그 결과로 자동 생성된 `id`가 `KeyHolder` 객체에 저장

# 6. 참고자료

- [Spring - JdbcTemplate > Querying](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#jdbc-JdbcTemplate-examples-query)
- [Spring - JdbcTemplate > Updating](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#jdbc-JdbcTemplate-examples-update)
