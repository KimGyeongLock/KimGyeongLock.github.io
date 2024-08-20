---
layout: single
title: "[Spring-DATA-JPA-2] Entity Relationships Mapping"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Entity Relationships Mapping

객체는 참조를 통해 관계를 정의하지만, 데이터베이스는 외래 키를 사용하여 테이블 관계를 정의합니다.    
엔티티 연관관계 매핑(Entity Relationship Mapping)은 두 데이터베이스 테이블 간의 관계를 도메인 모델의 속성으로 모델링합니다.    
즉, **데이터베이스 테이블 간의 관계를 객체 간의 관계로 매핑하는 것**을 의미합니다.    

엔티티 연관관계는 **일대일**, **다대일**, **다대다** 등 연결 방식으로 분류되기도 하며,    
연결 방향에 따라 엔티티가 상호 접근이 가능하면 **양방향**, 한쪽 방향으로만 접근이 가능하면 **단방향**으로 분류됩니다.    

엔티티 연관관계는 연결 방식과 연결 방향에 따라 다른 쿼리가 생성되며,    
간혹 의도하지 않은 쿼리가 생성되는 경우도 있습니다.    
따라서 상황에 따른 적절한 연결 방식과 연결 방향을 선택하는 것이 중요합니다.    

<img width="457" alt="image" src="https://github.com/user-attachments/assets/2eded9a5-7775-4361-a943-04295f8fd387">

---

# 2. 다대일 단방향

하나의 `Publisher`는 여러개의 `Book`을 가질 수 있는 **다대일 관계**를 예시가 있습니다.    
데이터베이스 테이블에서는 `Book` 테이블의 외래 키가 `Publisher` 테이블의 기본 키를 참조하게 설계하는게 일반적입니다.    
이 경우, 객체 설계 방법으로 `Book` 클래스에 `Publisher` 클래스를 참조하는 멤버 변수를 추가할 수 있습니다.    
다대일 관계의 멤버 변수를 설정 할 때는 `@ManyToOne` 어노테이션을 사용합니다.    
    
```java
@Entity
class Book {
    @Id @GeneratedValue
    Long id;

    @ManyToOne
    Publisher publisher;

    // ...
}

```

<img width="426" alt="image 1" src="https://github.com/user-attachments/assets/94a5441d-8f89-4ff7-83f9-c2020c2a0290">

- `book` 테이블에 `publisher_id`라는 외래 키 필드가 생성

<img width="403" alt="image 2" src="https://github.com/user-attachments/assets/c03944b5-24fe-408c-87b6-5c3b5d588b9f">

- `book` 테이블에 `publisher_id` 필드에 대한 외래 키 제약 조건이 추가
- `book` 테이블의 `publisher_id`가 `publisher` 테이블의 `id` 필드를 참조

---

# 3. 다대일 양방향

만약 특정 `Publisher`가 발행한 모든 책을 조회해야 한다면, `Publisher`도 `Book`을 멤버 변수로 관계를 맺으면 좋습니다.      
이 경우 `Book`이 `Publisher`에 의존하는 상황에서 `Publisher`도 `Book`에 의존하는 관계를 **양방향**이라고 합니다.     
양방향 연관관계를 만들기 위해서는, `Publisher` 클래스에 **콜렉션 값 속성을 추가**하고 이를 **@OneToMany**으로 지정합니다.     
이렇게 하면 `Book` 클래스와 `Publisher` 클래스 사이에 양방향 연관관계가 설정됩니다.     

양방향 연관관계임을 명확히 표시하고, 이미 지정된 매핑 정보를 재사용하기 위해서는 '**mappedBy**'를 사용해야 합니다.     

데이터베이스에서 테이블간의 관계를 맺을 때, **외래키를 가지는 테이블**을 **연관관계의 주인**이라고 합니다.     
엔티티 클래스에서도 연관관계의 주인을 지정해야 합니다.     
연관관계의 주인은 **mappedBy** 속성을 통해 지정할 수 있습니다.     
mappedBy 속성은 **연관관계의 주인이 아닌 엔티티 클래스**의 멤버 변수 이름을 지정해야 합니다.     

⇒ 정리

foreign key == `@ManyToOne Publisher publisher;`

연관관계의 주인 == foreign key를 가지는 테이블 == **book** table

- 실제로 데이터베이스에서 관계를 관리

연관관계의 주인이 아닌 엔티티 == **publisher** table == **mappedBy 속성을 사용**

- **mappedBy** : 주인이 되는 엔티티의 어떤 필드(멤버 변수)(foreign key)에 의해 매핑되는지를 지정
- 데이터베이스에 외래 키를 직접 관리하지 않으며, 단지 매핑 정보를 재사용

```java
@Entity
class Publisher {
    @Id @GeneratedValue
    Long id;

    @OneToMany(mappedBy="publisher")
    Set<Book> books;

    // ...
}

```

```java
@OneToMany
Book book; 
```

> 'One To Many' attribute type should be a container 
⇒  `Set<Book> books = new HashSet<>();`
> 

## 1). `mappedBy` 설정이 있는 경우 (`Publisher` 클래스)

```java
@Entity
public class Publisher {
    // ...
    @OneToMany(mappedBy="publisher")
    Set<Book> books = new HashSet<>();
    // ...
}

```

- **SQL 쿼리**: 이 경우, `Publisher`와 `Book` 사이의 관계에서 외래 키(`publisher_id`)는 `Book` 테이블에만 존재하며, `Publisher` 엔티티는 이를 단순히 참조합니다.
- **쿼리 생성**: `Book` 엔티티가 외래 키를 관리하므로, `Book`을 삽입할 때 외래 키(`publisher_id`)가 함께 삽입됩니다. `Publisher` 테이블에는 외래 키 관련 정보가 포함되지 않습니다.
- **쿼리 예시**:
    
    <img width="247" alt="image 3" src="https://github.com/user-attachments/assets/92ab6045-9d52-4948-aaf5-120ffb2a4d86">
    

## 2). `mappedBy` 설정이 없는 경우 (`Publisher` 클래스)

```java
@Entity
public class Publisher {
    // ...
    @OneToMany
    Set<Book> books = new HashSet<>();
    // ...
}

```

- **SQL 쿼리**: `mappedBy` 설정이 없으면 JPA는 `Publisher`와 `Book` 간의 양방향 관계를 **두 개의 독립적인 관계**로 인식합니다. 따라서 `Publisher` 테이블에 `books` 컬렉션을 표현하기 위한 **중간 테이블**이 생성될 수 있습니다.
- **쿼리 생성**: 이 경우, JPA는 `Publisher`와 `Book` 사이에 추가적인 관계를 관리하기 위해 연결 테이블을 생성할 수 있으며, 이로 인해 더 많은 쿼리가 발생합니다.
- **쿼리 예시**:
    
    <img width="286" alt="image 4" src="https://github.com/user-attachments/assets/e75e14b0-6351-48fa-aa5d-1439608ab51b">


다대일 관계 매핑 후 repository를 이용하여 데이터를 조회하면 어떤 쿼리가 생성되는지 확인해보세요.

`findById` - JPA repository에 포함

## JPA의 로딩 전략(`FetchType.EAGER` vs `FetchType.LAZY`)

`EAGER`는 즉시 로딩을 위해 `JOIN`을 사용하고, `LAZY`는 필요할 때만 데이터를 로딩하기 때문에 초기 쿼리에서는 `JOIN`이 사용되지 않습니다.

이 현상은 JPA에서의 연관관계 매핑과 로딩 전략(`fetch` 옵션)이 SQL 쿼리 생성에 어떻게 영향을 미치는지를 보여줍니다. 각각의 경우에 대해 설명하겠습니다.

### 1. `findByIdForBook` 메서드에서 `LEFT JOIN` 사용

```java
@ManyToOne
Publisher publisher;

```

- **설명**: `findByIdForBook` 메서드는 `Book` 엔티티를 조회합니다. 이때 `Book`은 `@ManyToOne` 관계를 통해 `Publisher`와 연결되어 있습니다.
- **기본 설정**: `@ManyToOne` 관계는 **기본적으로 `FetchType.EAGER`로 설정**되어 있습니다. 즉, **`Book` 엔티티를 조회할 때 연관된 `Publisher` 엔티티도 함께 로딩**됩니다.
- **SQL 쿼리**: 따라서 `Book`을 조회하는 쿼리가 실행될 때, `Publisher`를 함께 조회하기 위해 **`LEFT JOIN`이 사용**됩니다.

<img width="349" alt="image 5" src="https://github.com/user-attachments/assets/725382a4-6b62-48bb-a8ea-858d42b357a4">

### 2. `findByIdForPublisher` 메서드에서 `LEFT JOIN`이 사용되지 않음

```java
@OneToMany(mappedBy = "publisher")
Set<Book> books;

```

- **설명**: `findByIdForPublisher` 메서드는 `Publisher` 엔티티를 조회합니다. `Publisher`는 `@OneToMany` 관계를 통해 여러 `Book` 엔티티와 연결되어 있습니다.
- **기본 설정**: `@OneToMany` 관계는 기본적으로 `FetchType.LAZY`로 설정되어 있습니다. 즉, `Publisher`를 조회할 때 연관된 **`Book` 컬렉션은 즉시 로딩되지 않고, 실제로 접근할 때 로딩**됩니다.
- **SQL 쿼리**: `findByIdForPublisher` 메서드에서는 `Publisher`를 조회할 때 `LEFT JOIN`이 사용되지 않고, **단순히 `Publisher` 엔티티만 조회**됩니다. 이는 `Book` 컬렉션이 **지연 로딩**되기 때문입니다. 실제로 `Publisher.getBooks()`를 호출하기 전까지는 **`Book` 엔티티들이 로드되지 않습니다.**

<img width="224" alt="image 6" src="https://github.com/user-attachments/assets/f02caf21-a48a-49ce-a095-cd9154dbbb41">

### 3. `@OneToMany(mappedBy = "publisher", fetch = FetchType.EAGER)`로 설정 변경 후 `LEFT JOIN` 사용

```java
@OneToMany(mappedBy = "publisher", fetch = FetchType.EAGER)
Set<Book> books;

```

- **설명**: 여기서는 `@OneToMany` 관계에서 `fetch = FetchType.EAGER`로 설정이 변경되었습니다.
- **변경된 설정**: `FetchType.EAGER`로 설정하면 `Publisher`를 조회할 때 연관된 `Book` 엔티티들도 **즉시 로딩**됩니다.
- **SQL 쿼리**: 이로 인해 `findByIdForPublisher` 메서드를 실행할 때 `Publisher`와 관련된 `Book`들을 함께 조회하기 위해 `LEFT JOIN` 쿼리가 실행됩니다.

<img width="310" alt="image 7" src="https://github.com/user-attachments/assets/887302fd-f623-4f4e-a531-49c025039ddc">

- **Lazy Loading**: 연관된 엔티티를 필요할 때 로딩합니다. 성능 최적화에 유리하지만, 추가적인 쿼리가 발생할 수 있으며, 올바르게 사용하지 않으면 `LazyInitializationException`이 발생할 수 있습니다.
- **Eager Loading**: 연관된 엔티티를 즉시 로딩합니다. 모든 데이터를 한 번에 로딩하기 때문에 이후 쿼리를 줄일 수 있지만, 불필요한 데이터를 로딩할 위험이 있으며, 대규모 데이터에서는 성능 문제가 발생할 수 있습니다.

---

# 4. 일대일 단방향

일대일 관계는 **UNIQUE 제약 조건이 있는 외래 키 열에 매핑된다**는 점을 제외하면 @ManyToOne 연관과 거의 동일합니다.     
`Author` 테이블에는 연결된 `Person`의 식별자를 보유하는 외래키 컬럼이 있습니다.     

```java
@Entity
class Author {
    @Id @GeneratedValue
    Long id;

    @OneToOne
    Person person;

    // ...
}

```

<img width="431" alt="image 8" src="https://github.com/user-attachments/assets/c5a26c3b-5bbc-47bd-9738-1ce0c9eabddb">

- person_id column이 UNIQUE 제약 조건이 있는 외래 키 열에 매핑

# 5. 일대일 양방향

`Person` 엔터티의 `Author`에 대한 **참조를 다시 추가하여 이 연결을 양방향**으로 만들 수 있습니다.     
**mappedBy로 표시되지 않은 쪽**이 **의존 관계의 주인**이기 때문에, `Author` 엔티티의 author 멤버 변수에는 mappedBy 속성을 지정해야 합니다.    

```java
@Entity
class Person {
  @Id @GeneratedValue
  Long id;

  @OneToOne(mappedBy = "person")
  Author author;

  // ...
}

```

**auth table**

<img width="421" alt="image 9" src="https://github.com/user-attachments/assets/549281b6-0219-48aa-80a8-04a2874c5256">

- person_id 외래키를 가지고 있음
- 의존 관계의 주인

**person table**

<img width="421" alt="image 10" src="https://github.com/user-attachments/assets/f8d20adf-894f-437e-9ff1-1bd29fcc057f">

- mappedBy 속성 설정
- 의존 관계의 주인이 아닌 엔티티 클래스

## `mappedBy` 설정이 없는 경우

에러가 발생!

⇒ OneToOne의 경우 어느 테이블에 외래 키가 존재할지를 결정하기 위해, **반드시 두 엔티티 중 하나가 관계의 소유자**가 되어야 합니다.

`mappedBy` 속성이 없으면, **JPA는 두 엔티티가 각각의 외래 키를 소유한다**고 생각합니다. 이는 `OneToOne` 관계에서 불필요한 외래 키가 두 테이블에 생성될 수 있음을 의미하고, 데이터의 일관성을 유지할 수 없는 오류가 발생할 수 있습니다. 따라서 `mappedBy` 속성을 사용하여 양방향 관계에서 소유자와 대상 엔티티를 명확하게 지정해 주어야 합니다.

### ManyToOne의 경우

항상 Many쪽이 외래 키를 가진다!

즉, Many == 의존 관계의 주인, One == mappedBy를 붙인다.

다대일 관계 매핑 후 repository를 이용하여 데이터를 조회하면 어떤 쿼리가 생성되는지 확인해보세요.

- `findByIdForAuthor`

<img width="321" alt="image 11" src="https://github.com/user-attachments/assets/91e6fd24-0692-420b-88ac-d151e78c00e4">

- `findByIdForPerson`
    - @ManyToOne과 다르게 fetch 설정을 해주지 않아도 join이 포함되는 이유를 고민해보세요.
    - `@OneToOne` 관계의 기본 `fetch` 전략: `FetchType.EAGER`

<img width="324" alt="image 12" src="https://github.com/user-attachments/assets/6f2b4f7b-c39b-4ee4-9b2c-1aeae09ce29b">

- `@OneToOne(mappedBy = "person", fetch = FetchType.*LAZY*)`
    - `@OneToOne` 관계에서 `fetch = FetchType.LAZY`로 설정했음에도 불구하고 `left join`이 발생하는 것은 Hibernate가 성능 최적화와 데이터 무결성을 유지하기 위한 전략 중 하나입니다. 이를 통해 프록시 객체 사용 시 발생할 수 있는 비효율성이나 N+1 문제를 미리 방지하고, 관계된 엔티티의 즉각적인 접근을 가능하게 합니다. 이런 이유로 `LAZY` 설정에도 불구하고 `left join`을 사용하는 것이 JPA 구현체의 기본 동작일 수 있습니다.

---

# 6. 다대다

다대다 연관관계는 컬렉션 값 속성으로 표현됩니다.       
다대다 관계 매핑을 구현할 때 주의해야 할 점은 이런 관계가 **데이터베이스 스키마에서 직접적으로 표현되기 어렵다는 것**입니다.     
**대부분의 관계형 데이터베이스는 다대다 관계를 직접 지원하지 않으므로**,     
이를 구현하기 위해서는 보통 '**조인 테이블**' 또는 '**연결 테이블**'을 사용합니다.     
이 테이블은 두 엔티티 간의 관계를 연결하는 데 사용되며, **각 엔티티의 키를 외래 키로 포함**합니다.     

```java
@Entity
class Book {
    @Id @GeneratedValue
    Long id;

    @ManyToMany
    Set<Author> authors;

    // ...
}

```

양방향 연관관계인 경우, **mappedBy**를 지정하여 연관관계의 주인이 아님을 나타내야 합니다.     
이는 `Book` 측에서 설정된 속성이 연관관계에서 이미 정의된 매핑을 따른다는 것을 명시하는 것입니다.     

```java
@Entity
class Author {
    // ...

    @ManyToMany(mappedBy="authors")
    Set<Book> books;

    // ...
}

```

초기에는 `Author` 클래스와 `Book` 사이의 연관 관계를 명료하게 설정할 수 있지만,     
추가 정보가 필요해 지는 경우 연관 관계 테이블에 추가 열이 필요해집니다.     
추가 정보는 **연관 테이블**에 속해야 하는데, 이러한 속성들은 Book 속성이나 Author 속성으로 쉽게 저장할 수 없습니다.     
따라서 이 경우 연관 테이블에 대한 **새로운 엔티티 클래스를 도입**하는 것이 바람직합니다.     
예를 들어 'BookAuthor',에 저장되며, 이는 작가와 책 사이의 **@OneToMany** 및 **@ManyToOne** 연관관계로 매핑됩니다.     
이 접근법은 다대다 연관관계를 **중간 엔티티**를 사용하여 표현함으로써 추가 정보를 쉽게 관리할 수 있게 해줍니다.     

```java
@Entity
class BookAuthor {
    @Id @GeneratedValue
    Long id;

    @ManyToOne
    Book book;

    @ManyToOne
    Author author;

    // ...
}

```

```java
@Entity
class Book {
    // ...

    @OneToMany(mappedBy="book")
    Set<BookAuthor> authors;

    // ...
}

```

```java
@Entity
class Author {
    // ...

    @OneToMany(mappedBy="author")
    Set<BookAuthor> books;

    // ...
}

```

각 엔티티 - `@OneToMany`

중간 엔티티 - `@ManyToOne`

<img width="418" alt="image 13" src="https://github.com/user-attachments/assets/6cf08146-8143-454a-812d-54b24c5af7f7">

# 7. 참고자료

- [Jakarta Persistence - 2.10. Entity Relationships](https://jakarta.ee/specifications/persistence/3.2/jakarta-persistence-spec-3.2-m1#a516)
- [An Introduction to Hibernate 6 - 3.15. Associations](https://docs.jboss.org/hibernate/orm/6.4/introduction/html_single/Hibernate_Introduction.html#associations)
