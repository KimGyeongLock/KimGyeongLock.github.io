---
layout: single
title: "[Spring-MVC-3] 예외 처리"
toc: true
toc_sticky: true
categories: springlearningtest
published: true
---

# 1. Spring MVC 에서의 예외처리

Spring MVC 에서는 애플리케이션에서의 **예외를 효과적으로 관리**할 수 있도록 **@ExceptionHandler**, **@ControllerAdvice** 등의 어노테이션을 제공합니다.

이 문서에서는 각 어노테이션의 사용법을 설명하고, 실습할 수 있는 학습 테스트를 안내합니다.

# 2. @ExceptionHandler

**@ExceptionHandler**는 **특정 컨트롤러 내**에서 발생할 수 있는 예외를 처리하기 위한 메서드에 적용되는 어노테이션입니다.      
이 어노테이션이 적용된 메서드는 해당 컨트롤러에서 처리되지 않은 예외를 캐치하고, 그 예외에 대한 사용자 정의 처리 로직을 실행합니다.     

메서드는 예외 객체를 파라미터로 받을 수 있으며, 적절한 응답을 반환할 수 있습니다.  

```java
@Controller
public class MyController {
    @ExceptionHandler(value = NullPointerException.class)
    public ResponseEntity<String> handleNullPointerException(NullPointerException ex) {
        return new ResponseEntity<>("Null Pointer Exception occurred", HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

```

## 학습 테스트

- 테스트 메서드: `cholog.ExceptionTest.handleExceptionUsingExceptionHandler`
- 수행 방법
    - `cholog.controller.ProductController` 에 예외 처리 로직을 추가하여 학습 테스트를 성공시키세요.

`throw new IllegalArgumentException("Invalid keyword: " + keyword);`

⇒    

```java
@ExceptionHandler(IllegalArgumentException.class)
public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException ex) {
    return new ResponseEntity<>(ex.getMessage(), HttpStatus.BAD_REQUEST);
}
```

## 참조

- [Spring - Exceptions](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-exceptionhandler.html)

<br>

# 3. @ControllerAdvice

**@ControllerAdvice**는 **애플리케이션 전역**에서 발생하는 예외를 처리하기 위한 클래스에 적용되는 어노테이션입니다.      
이 어노테이션을 사용하면 여러 컨트롤러에 걸쳐 공통적으로 발생할 수 있는 예외를 한 곳에서 처리할 수 있습니다.     

@ExceptionHandler와 같은 다른 어노테이션과 결합하여 사용되며, 특정 패키지 내의 컨트롤러 또는 특정 타입의 컨트롤러에 대해서만 적용할 수도 있습니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
  @ExceptionHandler(value = Exception.class)
  public ResponseEntity<String> handleException(Exception ex) {
    return new ResponseEntity<>("An error occurred", HttpStatus.INTERNAL_SERVER_ERROR);
  }
}

```

## 학습 테스트

- 테스트 메서드: `cholog.ExceptionTest.handleExceptionUsingControllerAdvice`
- 수행 방법
    - `cholog.controller.ProductController`, `cholog.controller.MemberController` 를 수정하지 않고 학습 테스트를 성공시키세요.

`throw new NotFoundException("Member not found: id=" + id);` 

⇒    

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(NotFoundException.class)
    public ResponseEntity<String> handleNotFoundException(NotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}

```

> ChatGPT

`@ControllerAdvice`를 사용하여 전역 예외 처리기를 통해 모든 예외를 처리하는 방법이 확실히 편리하고 코드 중복을 줄여줍니다.       
그러나 클래스마다 `@ExceptionHandler`를 사용하는 이유도 있습니다. 아래는 클래스마다 `@ExceptionHandler`를 사용하는 주요 이유들입니다.     

1. **특정 컨트롤러에 대한 맞춤형 예외 처리**:
    - 특정 컨트롤러에 대해 개별적으로 맞춤형 예외 처리가 필요할 때 유용합니다. 예를 들어, 특정 컨트롤러에서 발생하는 예외에 대해 다른 컨트롤러와는 다른 메시지나 HTTP 상태 코드를 반환하고 싶을 때 사용할 수 있습니다.
2. **모듈화 및 유지보수 용이성**:
    - 예외 처리를 컨트롤러와 함께 정의하면 코드의 모듈화가 잘 이루어집니다. 이는 특정 컨트롤러의 예외 처리 로직을 수정해야 할 때 더 쉽게 유지보수할 수 있게 합니다.
3. **단일 책임 원칙 (SRP)**:
    - 각 컨트롤러가 자신의 예외를 처리하게 함으로써 단일 책임 원칙을 준수할 수 있습니다. 즉, 컨트롤러는 자신의 책임 범위 내에서 예외를 처리합니다.
4. **특정 예외에 대한 세부 제어**:
    - 특정 예외를 처리할 때 더 세부적으로 제어할 수 있습니다. 예를 들어, 예외에 따라 로깅, 메시지 변환, 추가 데이터 처리 등을 다르게 수행할 수 있습니다.
5. **점진적 마이그레이션**:
    - 기존 시스템에서 새로운 예외 처리 방식으로 점진적으로 마이그레이션할 때 유용할 수 있습니다. 모든 예외 처리를 한꺼번에 전역 처리기로 이동하는 대신, 점진적으로 각 컨트롤러에 맞춤형 예외 처리를 적용할 수 있습니다.

결론적으로, 전역 예외 처리기를 사용하는 것이 일반적으로 편리하고 중복 코드를 줄여주지만, 특정 상황에서는 각 컨트롤러마다 `@ExceptionHandler`를 사용하는 것이 더 적합할 수 있습니다. 프로젝트의 요구 사항과 구조에 따라 이 두 가지 방법을 적절히 혼합하여 사용하는 것이 좋습니다.
