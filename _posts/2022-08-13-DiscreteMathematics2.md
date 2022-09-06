---
layout: single
title: \[예습] Predicate Logic
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Predicate(술어)
: 변수에 대한 **propositional function(명제함수)**
* P(x): x(변수)에 대한 propositional function(P)의 값
* 값은 **True** or **False**으로 평가
* Ex) x + y = z : R(x, y, z)
  * R(2, -1, 5) = **F**, R(3, 4, 7) = **T**, R(x, 3, z) = **Not a Propostion**

-----------------

# Compound Expressions

P(3) **∨** P(-1) Solution: T<br/>
P(3) **∧** P(-1) Solution: F<br/>
P(3) **→** P(-1) Solution: F<br/>
<br/>
변수가 있는 표현식은 명제x -> No Value<br/>
P(3) ∧ P(**y**)<br>
P(**x**) → P(**y**)<br>

-----------------

# Quantification

**Quantifier(한정자)**
* 명제함수의 참, 거짓을 판별하기 위해 논의영역의 범위 정의
  * Like English words, **All** and **Some**
* Quantifiers have <u>higher precedence</u> than all logical operators 
  * ∀x P(x) ∨ Q(x) means (∀x P(x)) ∨ Q(x)

## Universal Quantification(전체 한정)
* 기호: **∀**(universal quantifier)
* 논의 영역(U, domain)에 속하는 **모든 값**을 의미
* 모든 𝑥에 대한 명제 P(x): **∀𝑥𝑃(𝑥)** 
* x > 0 and U is the integers, ∀𝑥𝑃(𝑥) is *false*
* x > 0 and U is the positive integers, ∀𝑥𝑃(𝑥) is *true*
* ∀𝑥𝑃(𝑥) ≡ P(1) ∧ P(2) ∧ ... ∧ P(N)

## Existential Quantification(존재 한정)
* 기호: **∃**(existential quantifier)
* 논의 영역(U)에 속하는 **어떤 값**을 의미
* 어떤 𝑥에 대한 명제 P(x): **∃𝑥𝑃(𝑥)**
* x > 0 and U is the integers, ∃𝑥𝑃(𝑥) is *true*
* x is even and U is the integers, ∃𝑥𝑃(𝑥) is *true*
* ∃𝑥𝑃(𝑥) ≡ P(1) ∨ P(2) ∨ ... ∨ P(N)


## Uniqueness Quantifier(유일 한정자)
* 기호: **∃!**
* 논의 영역(U)에 속하는 **단 하나의 값**을 의미
* 고유한 𝑥에 대한 명제 P(x): **∃!𝑥𝑃(𝑥)**

-----------------

# Translating from english to logic
Ex1) "Every student in this class has taken a course in C"<br/>
Solution 1: **∀x C(x)**<br/>
* domain U: all students in this class
* C(x): "x has taken a course in C"

Solution 2: **∀x (S(x) → C(x))**
* domain U: all people
* S(x): "x is a student in this class"
* C(x): "x has taken a course in C"

<br/>

Ex2) "Some student(s) in this class has taken a course in C."<br/>
Solution 1: **∃x C(x)**<br/>
* domain U: all students in this class
* C(x): "x has taken a course in C"

Solution 2: **∃x (S(x) ∧ C(x))**
* domain U: all people
* S(x): "x is a student in this class"
* C(x): "x has taken a course in C"


## **∧와 →의 차이**<br/>
∀y(y≠0→y^3≠0): True<br/>
∀y(y≠0∧y^3≠0): False<br/>
∀x(S(x) ∧ C(x)): **모든** 실수가 P(x)를 만족하지 않을 수도 있으므로 의도와 다르게 사용됨
* 모든 학생들은 이  학생이고, 모든 학생들은 C 수업을 들었다.

∃x(S(x) → C(x)): **어떤** 실수가 P(x)를 만족하지 않을 수도 있으므로 의도와 다르게 사용됨
* 어떤 학생이 이 반의 학생이라면, C 수업을 들었을 것이다.

-----------------

# Equivalences in Predicate logic
if predicate statements  have the same truth value, they are logically equivalent
* ∀x(P(x) ∧ Q(x)) ≡ ∀xP(x) ∧ ∀xQ(x)
* ∃x(P(x) ∨ Q(x)) ≡ ∃xP(x) ∨ ∃xQ(x)

## Negating Quantified Expressions
De Morgan’s Laws for Quantifiers.
|Negation|Equivalent Statement|
|:---:|:---:|
|¬∃xP(x)|∀x¬P(x)|
|¬∀xP(x)|∃x¬P(x)|

-----------------

# Nested Quantifiers(중첩 한정자)
∀x(∃y(x + y = 0))<br/>
한정자의 순서는 값에 영향을 미침<br>
* **∀x**(**∃y**(x + y = 0)): 모든 x에 대해 “x + y = 0”을 만족하는 y가 존재한다 -> **True**
* **∃y**(**∀x**(x + y = 0)): 어떤 y에 대해 모든 x가 “x + y = 0”을 만족하는 y가 존재한다 -> **False**

-----------------

# Negating Nested Quantifiers
∀w¬∀a∃f(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a¬∃f(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a∀f¬(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a∀f(¬P(w, f) ∨ ¬Q(f, a))<br>
