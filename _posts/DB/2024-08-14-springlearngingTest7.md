---
layout: single
title: "[Spring-Core-1] Spring Bean, Dependency Injection(DI), Component Scan"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Spring Bean

스프링은 애플리케이션의 복잡성을 줄이고 유지보수를 용이하게 하기 위해 **객체의 생성, 설정 및 생명주기를 관리**하는 **스프링 컨테이너(Spring(IOC) Container)**를 제공합니다.    
이 컨테이너가 관리하는 객체를 **스프링 빈**이라고 하며, 이를 통해 의존성 주입 및 객체 관리가 자동화됩니다.    

⇒ Spring Bean : 애플리케이션의 복잡성을 줄이고 유지보수를 용이하게 해준다.    

## 1.1. Bean Registration

스프링에서 **빈을 등록**하는 방법은 다양한데, 그 중 애너테이션을 이용한 방법으로 클래스에 `@Component` 어노테이션을 추가하는 방법이 있습니다.

```java
@Component
public class SpringBean {
}

```

```java
@Configuration
public class SpringBean {
    @Bean
    public String hello() {
        return "Hello";
    }
}
```

- `@Bean` 이라는 어노테이션이 있는 것을 알고 있어서 써 보았고 똑같이 기능 함을 알수 있었다.

### 그렇다면 @Bean과 @Component의 차이가 뭘까?

- `@Bean` : 개발자가 직접 제어가 불가능한 외부 라이브러리등을 Bean으로 등록하기 위한 어노테이션
    - 메소드 레벨에서 선언
    - 반환되는 객체(인스턴스)를 수동으로 빈으로 등록
    - ex) **RestTemplate**
- `@Component` : 개발자가 직접 작성한 Class를 Bean으로 등록하기 위한 어노테이션
    - 클래스 레벨에서 선언
    - 스프링이 런타임시에 **컴포넌트스캔**을 하여 자동으로 빈을 찾고(detect) 등록

출처: [https://galid1.tistory.com/494](https://galid1.tistory.com/494) [배움이 즐거운 개발자:티스토리]

참고: [https://curiousjinan.tistory.com/entry/spring-bean-component](https://curiousjinan.tistory.com/entry/spring-bean-component)

## 1.2 Bean Autowiring

스프링 컨테이너에 등록된 객체는 매번 새로이 생성할 필요없이 **컨테이너에서 가져와서 사용**할 수 있습니다.

**<필드 주입(Field Injection)>**

```java
@Autowired
private SpringBean springBean;

```

`@Autowired` 어노테이션을 사용하면, 스프링이 해당 필드, 생성자, 또는 메서드에 필요한 빈을 자동으로 주입합니다. 개발자가 **명시적으로 객체를 생성하고 주입할 필요 없이, 스프링 컨테이너가 이를 관리**합니다.

### 장점

- **의존성을 낮추고** 유연성을 높인다.
    
    참고: [https://maivve.tistory.com/184](https://maivve.tistory.com/184)
    
- setter 메서드를 작성하거나, 생성자에서 빈을 직접 주입받는 등의 반복적인 코드를 줄일 수 있습니다. 이는 코드의 간결성과 가독성을 향상시킨다.

### `@Autowired` 어노테이션을 사용하지 않는 경우

**1. 직접 객체 생성 (Manual Dependency Injection)**

`@Autowired`를 사용하지 않으면, 객체를 직접 생성해서 주입해야 합니다. 이 경우, 클래스 내부에서 필요한 의존성을 직접 초기화하게 됩니다.

```java
public class AutowiredBean {
    
    private SpringBean springBean = new SpringBean();

    public String sayHello() {
        return springBean.hello();
    }
}

```

- 결합도가 높아지며, 클래스 간의 의존성이 강해집니다.
- 테스트나 유지보수가 어려워질 수 있습니다.

**2. 생성자 주입 (Constructor Injection)**

의존성을 생성자를 통해 주입받을 수도 있습니다. 이 방법은 테스트 가능성을 높이고, 의존성 주입의 유연성을 증가 시킵니다.

```java
public class AutowiredBean {

	private SpringBean springBean;
	
	public AutowiredBean(SpringBean springBean) {
	    this.springBean = springBean;
	}
	
	public String sayHello() {
	    return springBean.hello();
	}
}
```

**3. 선택적인 의존성 주입 (Setter Injection)**

코드가 좀 더 유연해질 수 있으며, 의존성을 선택적으로 주입하거나 나중에 변경할 수 있습니다.

```java
@Component
public class AutowiredBean {

    private SpringBean springBean;

    // Setter 주입
    @Autowired
    public void setSpringBean(SpringBean springBean) {
        this.springBean = springBean;
    }

    public String sayHello() {
        return springBean.hello();
    }
}
```

스프링에서는 일반적으로 **생성자 주입(CI)을 권장**하는데, 그 이유는 의존성이 명확하게 드러나고, 단위 테스트가 용이하기 때문입니다. 필드 주입은 간결한 코드가 필요하거나 선택적 의존성을 다룰 때 주로 사용됩니다.

참고: [왜 Constructor Injection을 사용해야 하는가?](https://tecoble.techcourse.co.kr/post/2020-07-18-di-constuctor-injection/)

> 어쩌다 보니 아래에서 해야할 것을 미리 공부해버렸다

---

# 2. Dependency Injection

스프링 컨테이너에 등록된 스프링 빈 간의 의존성을 관리하는 방법은 다양합니다.    
그 중 애너테이션을 이용한 방법으로 **생성자**, **세터**, **필드**에 `@Autowired` 어노테이션을 추가하는 방법이 있습니다.    

## 2.1. Constructor Injection

스프링 컨테이너에 등록된 스프링 빈 간의 **의존성을 생성자를 통해 주입**하는 방법입니다.

```java
private InjectionBean injectionBean;

public ConstructorInjection(InjectionBean injectionBean) {
    this.injectionBean = injectionBean;
}

```

## 2.2. Setter Injection

스프링 컨테이너에 등록된 스프링 빈 간의 의존성을 **세터를 통해 주입**하는 방법입니다.

```java
private InjectionBean injectionBean;

@Autowired
public void setInjectionBean(InjectionBean injectionBean) {
    this.injectionBean = injectionBean;
}

```

### Setter 함수에 @Autowired를 붙여야 하는 이유

1. **Autowired 어노테이션의 역할**:
`@Autowired` 어노테이션은 스프링에게 해당 필드나 메서드에 의존성을 주입하라는 신호를 줍니다. 스프링은 이 어노테이션이 붙어있는 필드, 생성자, 또는 메서드를 확인하고, 그 타입에 맞는 빈(Bean)을 찾아 자동으로 주입합니다.
2. **Setter Injection에서의 동작**:
Setter Injection을 사용할 때, `@Autowired` 어노테이션이 Setter 메서드에 붙어 있지 않으면, 스프링은 그 메서드를 통해 의존성을 주입하라는 지시를 받지 않습니다. 따라서 스프링이 해당 메서드를 호출하여 의존성을 주입하도록 하기 위해 `@Autowired`를 반드시 명시해야 합니다.

## 2.3. Field Injection

스프링 컨테이너에 등록된 스프링 빈 간의 의존성을 필드를 통해 주입하는 방법입니다.

```java
@Autowired
private InjectionBean injectionBean;

```

### Field injection is not recommended

warning이 뜨는 이유는 Constructor Injection을 더 추천하기 때문이다!

**Field Injection**이 객체 지향 설계 원칙과 테스트 용이성 측면에서 몇 가지 단점을 가지고 있기 때문입니다.

참고: [왜 Constructor Injection을 사용해야 하는가?](https://tecoble.techcourse.co.kr/post/2020-07-18-di-constuctor-injection/)

---

# 3. Component Scan

스프링 컨테이너에 등록된 스프링 빈을 자동으로 찾아서 등록하는 방법입니다.

## 3.1. @ComponentScan

`@ComponentScan` 어노테이션을 이용하여 **스캔할 패키지를 지정**할 수 있습니다.    
앞서 수행한 학습 테스트에서 `@ComponentScan`을 사용하지 않고도 정상동작했던 이유는 `@SpringBootApplication`이 `@ComponentScan`을 포함하고 있기 때문입니다.    

```java
...
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
        @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
  ...
}

```

`@ComponentScan(basePackages = "cholog.scan")`

- 스프링이 `cholog.scan` 패키지 내의 모든 `@Component` 어노테이션이 붙은 클래스를 스캔하고 빈으로 등록하도록 지시합니다.
- `@Repository` 어노테이션을 사용하는 것도 가능
- `@Component` 어노테이션 및 `streotype(@Service, @Repository, @Controller.)` 어노테이션이 부여된 Class들을 자동으로 Scan하여 Bean으로 등록해주는 역할을 하는 어노테이션
출처: [https://galid1.tistory.com/510](https://galid1.tistory.com/510) [배움이 즐거운 개발자:티스토리]

### `@Repository`와 `@Component`의 차이점

- **@Component**: 스프링이 관리할 일반적인 빈(Bean)으로 등록되며, 특별한 역할 없이 빈을 나타냅니다.
- **@Repository**: 데이터 액세스 계층의 빈으로 사용되며, `@Component`의 기능을 확장하여 데이터 접근 관련 예외를 스프링 예외로 변환하는 기능을 포함합니다.

---

# 4. 참고자료

- [Spring - @Component](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-stereotype-annotations)
- [Spring - Dependencies](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-dependencies)
- [Spring - Constructor Injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-constructor-injection)
- [Spring - Setter Injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-setter-injection)
- [Spring - Field Injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-autowired-annotation)
