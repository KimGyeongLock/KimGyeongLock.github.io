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

# Compound Expressions

P(3) **∨** P(-1) Solution: T<br/>
P(3) **∧** P(-1) Solution: F<br/>
P(3) **→** P(-1) Solution: F<br/>
<br/>
변수가 있는 표현식은 명제x -> No Value<br/>
P(3) ∧ P(**y**)<br>
P(**x**) → P(**y**)<br>

# Quantification

**Quantifier(한정자)**
* 명제함수의 참, 거짓을 판별하기 위해 논의영역의 범위 정의
  * Like English words, **All** and **Some**
* Quantifiers have <u>higher precedence</u> than all logical operators 

## Universal Quantification(전체 한정)
* 기호: **∀**(universal quantifier)
* 논의 영역(U)에 속하는 **모든 값**을 의미
* 모든 𝑥에 대한 명제 P(x): **∀𝑥𝑃(𝑥)** 
* x > 0 and U is the integers, ∀𝑥𝑃(𝑥) is *false*
* x > 0 and U is the positive integers, ∀𝑥𝑃(𝑥) is *true*


## Existential Quantification(존재 한정)
* 기호: **∃**(existential quantifier)
* 논의 영역(U)에 속하는 **어떤 값**을 의미
* 어떤 𝑥에 대한 명제 P(x): **∃𝑥𝑃(𝑥)**
* x > 0 and U is the integers, ∃𝑥𝑃(𝑥) is *true*
* x is even and U is the integers, ∃𝑥𝑃(𝑥) is *true*


## Uniqueness Quantifier(유일 한정자)
* 기호: **∃!**
* 논의 영역(U)에 속하는 **단 하나의 값**을 의미
* 고유한 𝑥에 대한 명제 P(x): **∃!𝑥𝑃(𝑥)**

# Equivalences in Predicate logic
if predicate statements  have the same truth value, they are logically equivalent
* ∀x(P(x) ∧ Q(x)) ≡ ∀xP(x) ∧ ∀xQ(x)
* ∃x(P(x) ∨ Q(x)) ≡ ∃xP(x) ∨ ∃xQ(x)
* ¬∀xP(x) ≡ ∃x¬P(x)
* ¬∃xP(x) ≡ ∀x¬P(x)

# Nested Quantifiers(중첩 한정자)
∀x(∃y(x + y = 0))<br/>
한정자의 순서는 값에 영향을 미침<br>
* **∀x**(**∃y**(x + y = 0)): 모든 x에 대해 “x + y = 0”을 만족하는 y가 존재한다 -> **True**
* **∃y**(**∀x**(x + y = 0)): 어떤 y에 대해 모든 x가 “x + y = 0”을 만족하는 y가 존재한다 -> **False**

# Negating Nested Quantifiers
∀w¬∀a∃f(P(w, f) ∧ Q(f, a))
  ≡ ∀w∃a¬∃f(P(w, f) ∧ Q(f, a))
  ≡ ∀w∃a∀f¬(P(w, f) ∧ Q(f, a))
  ≡ ∀w∃a∀f(¬P(w, f) ∨ ¬Q(f, a))
