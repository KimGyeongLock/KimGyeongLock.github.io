---
layout: single
title: "[Spring-DATA-JPA-1] JPA, Repository"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. JPA, Spring Data JPA
 
JPA는 Java(현재는 Jakarta) Persistence API의 약자로서, 영속성 관리 및 객체/관계형 매핑을 위한 API의 명세입니다.     
Java 애플리케이션 개발자가 Java **도메인 모델**을 사용하여 **관계형 데이터베이스를 관리할 수 있도록 객체/관계형 매핑 기능을 제공**합니다.     
JPA를 통해 개발자는 데이터베이스와의 상호작용을 객체 지향적 방식으로 수행할 수 있으며, 복잡한 SQL 쿼리를 작성하지 않고도 데이터를 효율적으로 관리할 수 있습니다.     
     
Spring Data JPA는 JPA 기반 리포지토리를 쉽게 구현할 수 있게하여,     
데이터 액세스 기술을 사용하는 Spring 기반 애플리케이션을 더 쉽게 구축할 수 있게 도와줍니다.     

Spring Data JPA를 사용하기 위해서는 spring-boot-starter-data-jpa를 활용할 수 있고,     
여기엔 JPA의 구현 프로젝트인 Hibernate를 포함하고 있습니다.     

JPA 관련 학습 테스트를 처음 접하는 분들은 JPA와 Spring Data JPA을 구체적으로 구분하는 것과 같이 이론적인 부분에 많은 시간을 쓰기 보다는,     
학습 테스트를 통해 기능을 먼저 동작하게 한 후 이론 적인 내용을 학습하는 것을 추천드립니다.     

-----

# 2. EntityMapping

엔티티는 JPA에서 관리하는 객체입니다. 이 객체는 데이터베이스의 테이블과 매핑되어 있으며,     
JPA를 통해 데이터베이스에 저장되고 조회될 수 있습니다.     
이처럼 **객체를 테이블과 매핑** 하는 것을 **엔티티 매핑**이라 하고,     
아래에 소개된 애너테이션을 사용할 수 있습니다.     

- @Entity: 클래스가 **JPA 엔티티**임을 나타냅니다.     
- @Id: 엔티티의 **기본 키**를 나타냅니다.     
- @GeneratedValue: 기본 키 값 생성 **전략**을 지정합니다.     

```java
@Entity
public class Customer {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  // ...
}

```

## 학습 테스트

- 테스트 메서드:
    - `cholog.EntityManagerTest.persist`
    - `cholog.EntityManagerTest.flush`
- 수행 방법
    - `cholog.Customer` 을 이용하여 학습 테스트를 성공시키세요.
    - Customer 클래스에 @Entity, @Id 어노테이션을 활용하세요.

------

# 3. Repository

Spring Data JPA는 리포지토리 인터페이스를 통해 엔티티에 대한 CRUD 작업을 수행하는 메서드를 제공합니다.     

```java
public interface CustomerRepository extends CrudRepository<Customer, Long> {
}

```

## 학습 테스트

- 테스트 클래스: `cholog.RepositoryTest`
- 수행 방법
    - `cholog.CustomerRepository` 을 이용하여 학습 테스트를 성공시키세요.
    - CustomerRepository 인터페이스를 생성하고, CrudRepository를 상속하세요.
    - CrudRepository가 제공하는 메서드를 활용하세요.

<br>

`JpaRepository` vs `CrudRepository`

- `CrudRepository`
    - 기본적인 CRUD 작업을 수행
    - **주요 메서드:**
        - `save(S entity)`: 엔티티를 저장(삽입 또는 업데이트)합니다.
        - `findById(ID id)`: 주어진 ID로 엔티티를 조회합니다.
        - `findAll()`: 모든 엔티티를 조회합니다.
        - `deleteById(ID id)`: 주어진 ID의 엔티티를 삭제합니다.
        - `count()`: 엔티티의 총 개수를 반환합니다.
- `JpaRepository`
    - `CrudRepository`를 확장하는 인터페이스
    - **`CrudRepository`에서 상속받은 메서드 + 추가 메서드:**
        - `saveAll(Iterable<S> entities)`: 여러 엔티티를 한 번에 저장합니다.
        - `findAll(Sort sort)`: 정렬 기준을 적용하여 모든 엔티티를 조회합니다.
        - `findAll(Pageable pageable)`: 페이징 기능을 사용하여 엔티티를 조회합니다.
        - `flush()`: 현재 영속성 컨텍스트의 변경 내용을 데이터베이스에 즉시 반영합니다.
        - `saveAndFlush(S entity)`: 엔티티를 저장하고 즉시 데이터베이스에 반영합니다.
        - `deleteInBatch(Iterable<T> entities)`: 주어진 엔티티들을 일괄 삭제합니다.

------

# 4. Query Creation

Spring Data JPA는 메서드 **이름을 분석**하여 **쿼리를 생성**하는 기능을 제공합니다.     

```java

public interface CustomerRepository extends CrudRepository<Customer, Long> {
  List<Customer> findByLastName(String lastName);
}

```

## 학습 테스트

- 테스트 클래스: `cholog.QueryCreationTest`
- 수행 방법
    - `cholog.CustomerRepository` 을 이용하여 학습 테스트를 성공시키세요.
    - CustomerRepository에 테스트를 성공시키기 위해 메서드를 추가하세요.
    - 로그를 통해 쿼리가 생성되는 것을 확인하세요.

<br>

**메서드를 구현하지 않아도** 자동으로 이름을 분석하여 쿼리 생성     

<img width="230" alt="image" src="https://github.com/user-attachments/assets/2855e46f-4242-4eb2-9baa-3caf39aebd58">

------

# 5. 참고자료

- [Jakarta Persistence - 1. Introduction](https://jakarta.ee/specifications/persistence/3.2/jakarta-persistence-spec-3.2-m1#introduction)
- [Spring Data JPA - Getting Started(Entity Mapping)](https://docs.spring.io/spring-data/jpa/reference/jpa/getting-started.html)
- [Spring Data JPA - Core concepts(CrudRepository Interface)](https://docs.spring.io/spring-data/jpa/reference/repositories/core-concepts.html)
- [Spring Data JPA - Defining Query Methods > Query Creation](https://docs.spring.io/spring-data/jpa/reference/repositories/definition.html)

------

# 6. 코드
<https://github.com/KimGyeongLock/spring-learning-test/tree/roki/spring-data-jpa-1/spring-data-jpa-1/initial>
