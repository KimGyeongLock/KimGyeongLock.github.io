---
layout: single
title: "[Spring-Core-2] 환경 변수 설정, Profile"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Java-based Configuration

[spring-core-1](https://kimgyeonglock.github.io/springlearningtest/springlearngingTest7/)에서는 `@Component`, `@Autowired` 어노테이션을 사용해 스프링 빈을 생성하고 빈간 의존성을 주입하는 방법을 익혔습니다.

이 문서에서는 **Java 코드와 스프링이 제공하는 어노테이션**을 사용해 **스프링 컨테이너를 정의**하는 법을 알아봅니다.

## 1.1. Declaring a Bean

`@Configuration` 어노테이션이 달린 클래스와 `@Bean` 어노테이션이 달린 메서드를 통해 Java 코드에서 스프링 빈을 등록할 수 있습니다.

가장 단순한 `@Configuration` 클래스는 다음과 같습니다.

```java
@Configuration
public class AppConfig {
  @Bean
  public MyServiceImpl myService() {
    return new MyServiceImpl();
  }
}

```

### @Bean과 @Component의 차이가 뭘까?

- `@Bean` : 개발자가 직접 제어가 불가능한 외부 라이브러리등을 Bean으로 등록하기 위한 어노테이션
    - 메소드 레벨에서 선언
    - 반환되는 객체(인스턴스)를 수동으로 빈으로 등록
    - ex) **RestTemplate**
- `@Component` : 개발자가 직접 작성한 Class를 Bean으로 등록하기 위한 어노테이션
    - 클래스 레벨에서 선언
    - 스프링이 런타임시에 **컴포넌트스캔**을 하여 자동으로 빈을 찾고(detect) 등록

출처: [https://galid1.tistory.com/494](https://galid1.tistory.com/494) [배움이 즐거운 개발자:티스토리]

참고: [https://curiousjinan.tistory.com/entry/spring-bean-component](https://curiousjinan.tistory.com/entry/spring-bean-component)

## 1.2 Bean Dependencies

`@Configuration` 어노테이션이 있는 클래스 내의 메서드는 같은 클래스 내의 다른 `@Bean` 메서드를 호출하여 빈 간의 의존성을 정의할 수 있습니다.

```java
@Configuration
public class AppConfig {

  @Bean
  public BeanOne beanOne() {
    return new BeanOne(beanTwo());
  }

  @Bean
  public BeanTwo beanTwo() {
    return new BeanTwo();
  }
}

```

- `BeanOne`이 `BeanTwo`에 의존하고 있다

다른 `@Configuration` 클래스 내의 빈을 사용해서도 의존성을 정의할 수 있습니다. 

이 방법에 대해서는 [Spring - Bean Dependencies](https://docs.spring.io/spring-framework/reference/core/beans/java/bean-annotation.html#beans-java-dependencies) 문서를 참고해 주세요.

---

# 2. Property

프로퍼티는 애플리케이션의 구성값을 **키-값** 쌍으로 저장합니다. 예를 들어, 데이터베이스 연결 정보나 API 키 같은 설정값입니다.

스프링의 `Environment` 인터페이스는 이러한 **프로퍼티 소스들을 통합하여 관리**하고, 필요한 프로퍼티 값을 **조회**하는 기능을 제공합니다.

## 2.1. Using @PropertySource and Environment

`@PropertySource` 어노테이션을 사용해 프로퍼티 파일을 로드하고 `Environment`를 사용해 프로퍼티 값을 읽어올 수 있습니다.

```java
@Configuration
@PropertySource("classpath:/com/myco/app.properties")
public class AppConfig {

  @Autowired
  Environment env;

  @Bean
  public TestBean testBean() {
    TestBean testBean = new TestBean();
    testBean.setName(env.getProperty("testbean.name"));
    return testBean;
  }
}

```

1. Java-based Configuration을 하기 위한 클래스로 지정하기 
    
    ⇒ `@Configuration`
    
2. ext-api.properties 파일을 활용하기 위한 설정 추가하기 
    
    ⇒ `@PropertySource("classpath:ext-api.properties")`
    

`@PropertySource("classpath:ext-api.properties")`

- Spring 애플리케이션에서 `src/main/resources` 폴더는 자동으로 클래스패스에 추가되며, 파일을 클래스패스의 루트 경로를 기준으로 참조

1. ext-api.properties의 google.api.endpoint 값을 Environment를 사용해서 가져오기 
    
    ⇒ `env.getProperty("google.api.endpoint")`
    
2. 위 endpoint 값을 사용하여 GoogleMapsRestClient를 빈으로 등록하기 
    
    ⇒ `@Bean` 등록
    

## 2.2. Using @PropertySource and @Value

`@PropertySource`를 사용해 로드한 프로퍼티 파일의 값을 **`@Value` 어노테이션을 통해 주입**할 수 있습니다.

```java
@Configuration
@PropertySource("classpath:/com/myco/app.properties")
public class AppConfig {
  @Bean
  public TestBean testBean(@Value("${testbean.name}") String name) {
    TestBean testBean = new TestBean();
    testBean.setName(name);
    return testBean;
  }
}

```

- testbean.name 값을 `name` 변수에 주입

1. ext-api.properties의 google.api.endpoint 값을 어노테이션을 사용해서 가져오기 
    
    ⇒ `@Value`
    
2. 위 endpoint 값을 사용하여 GoogleMapsRestClient를 빈으로 등록하기 
    
    ⇒ `@Bean`
    

## 2.3. Externalized Configuration (Spring Boot)

프로퍼티 값을 설정하는 방법은 `@PropertySource` 외에도 다양합니다.       

특히 Spring Boot 를 사용한다면 `application.properties`(혹은 `application.yaml`) 파일을 사용해 프로퍼티 값을 편하게 설정할 수 있습니다.        

1. Java-based Configuration을 하기 위한 클래스로 지정하기
    
    ⇒ `@Configuration`
    
2. application.properties의 security.jwt.token.secret-key 값을 활용하여 JwtTokenKeyProvider를 빈으로 등록하기
    
    ⇒ `@Value("${security.jwt.token.secret-key}")`
    

---

# 3. Profile

프로파일은 애플리케이션 설정의 논리적인 그룹입니다. 예를 들어, 개발(development), 테스트(testing), 운영(production)과 같이 다른 환경에 적합한 설정을 분리할 수 있습니다.          

프로파일을 사용하면 같은 애플리케이션이지만 **환경에 따라 다른 구성을 적용**할 수 있습니다.          

스프링이 제공하는 `Environment` 인터페이스는 **현재 활성화되어 있는 프로파일**과 **기본 프로파일**을 관리합니다.        

## 3.1. @Profile

`@Profile` 어노테이션을 이용하여 특정 프로파일에 따라 빈을 등록할 수 있습니다.        
`@Profile` 어노테이션은 클래스 레벨, 메서드 레벨에 모두 적용 가능합니다.

### @Configuration 클래스에 적용하는 경우

클래스 내에서 정의된 Bean들은 `development` profile일 때만 등록됩니다.

```java
@Configuration
@Profile("development")
public class StandaloneDataConfig {

	@Bean
	public DataSource dataSource() {
		return new EmbeddedDatabaseBuilder()
			.setType(EmbeddedDatabaseType.HSQL)
			.addScript("classpath:com/bank/config/sql/schema.sql")
			.addScript("classpath:com/bank/config/sql/test-data.sql")
			.build();
	}
}

```

### @Bean 메서드에 적용하는 경우

profile에 따라 등록되는 Datasource Bean이 달라집니다.

```java
@Configuration
public class AppConfig {

  @Bean("dataSource")
  @Profile("development")
  public DataSource standaloneDataSource() {
    return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .addScript("classpath:com/bank/config/sql/test-data.sql")
            .build();
  }

  @Bean("dataSource")
  @Profile("production")
  public DataSource jndiDataSource() throws Exception {
    Context ctx = new InitialContext();
    return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
  }
}

```

1. Java-based Configuration을 하기 위한 클래스로 지정하기 
    
    ⇒ `@Configuration`
    
2. dev프로파일일 때만 InmemoryMessageRepository빈이 등록되도록 설정하기 
    
    ⇒ `@Bean("datasource")`, `@Profile("dev")`
    
3. prod 프로파일일 때만 InmemoryMessageRepository 빈이 등록되도록 설정하기 
    
    ⇒ `@Bean("datasource")`,  `@Profile("prod")`
    

# 4. 더 생각해보기

- 스프링 컨테이너를 정의하는 방법은 다양합니다.`@Component`, `@Autowired` 어노테이션을 사용하는 방법과 비교하여 Java 코드로 빈을 관리할 때의 장단점에 대해 생각해보고, 어떤 상황에서 어떤 방식을 택할지 고민해보세요.
- 이 외에도 XML을 사용해 스프링 컨테이너를 정의할 수도 있습니다. XML을 사용하는 방법에 대해 알아보고, Java 코드와 XML을 사용하는 방법을 비교해보세요.
- Spring Boot는 프로퍼티 파일 컨벤션(`application-{profile}`)을 사용해 활성 프로파일에 대한 프로퍼티 파일을 로드합니다. 예를 들어, 활성 프로파일이 prod 라면 `application.properties`, `application-prod.properties` 파일을 로드합니다. 이러한 특성을 사용해 어떤 값을 프로퍼티 파일에서 관리할지 생각해 보세요.

# 5. 참고자료

- [Spring - @Configuration](https://docs.spring.io/spring-framework/reference/core/beans/java/configuration-annotation.html)
- [Spring - @Bean](https://docs.spring.io/spring-framework/reference/core/beans/java/bean-annotation.html)
- [Spring - @PropertySource](https://docs.spring.io/spring-framework/reference/core/beans/environment.html#beans-using-propertysource)
- [Spring Boot - Externalized Configuration](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config)
- [Spring - @Value](https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/value-annotations.html)
- [Spring - @Profile](https://docs.spring.io/spring-framework/reference/core/beans/environment.html#beans-definition-profiles-java)
- [Spring Boot - Profile Specific Files](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config.files.profile-specific)
