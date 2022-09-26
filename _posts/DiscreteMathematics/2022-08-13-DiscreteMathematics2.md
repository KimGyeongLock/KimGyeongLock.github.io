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
  * "P at x" or "P of x" 
* 값은 **True** or **False**으로 평가
* Ex) x + y = z : R(x, y, z)
  * R(2, -1, 5) = **F**
  * R(3, 4, 7) = **T**
  * R(x, 3, z) = **Not a Propostion**

-----------------

# Compound Expressions

P(x) denotes “x > 0"<br/>
P(3) **∨** P(-1) Solution: T<br/>
P(3) **∧** P(-1) Solution: F<br/>
P(3) **→** P(-1) Solution: F<br/>
<br/>
변수가 있는 표현식은 명제x -> No Value<br/>
P(3) ∧ P(**y**)<br>
P(**x**) → P(**y**)<br>

*P(x)는 propositional function이지만 true/false를 갖지 않음*<br/>
*그러나 **quantifier**를 이용하면 true/false라고 말할 수 있음* 

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
  * "For all x, P(x)" or "For every x, P(x)"
* x > 0 and U is the integers, ∀𝑥𝑃(𝑥) is *false*
* x > 0 and U is the positive integers, ∀𝑥𝑃(𝑥) is *true*
* ∀𝑥𝑃(𝑥) ≡ P(1) ∧ P(2) ∧ ... ∧ P(N)

## Existential Quantification(존재 한정)
* 기호: **∃**(existential quantifier)
* 논의 영역(U)에 속하는 **어떤 값**을 의미
* 어떤 𝑥에 대한 명제 P(x): **∃𝑥𝑃(𝑥)**
  * "For some x, P(x)" or "For at least one x, P(x)"
* x > 0 and U is the integers, ∃𝑥𝑃(𝑥) is *true*
* x is even and U is the integers, ∃𝑥𝑃(𝑥) is *true*
* ∃𝑥𝑃(𝑥) ≡ P(1) ∨ P(2) ∨ ... ∨ P(N)


## Uniqueness Quantifier(유일 한정자)
* 기호: **∃!**
* 논의 영역(U)에 속하는 **단 하나의 값**을 의미
* 고유한 𝑥에 대한 명제 P(x): **∃!𝑥𝑃(𝑥)**


## Quantifiers and Evaluating them as Looping
* domain is finite
* ∀𝑥𝑃(𝑥) loop
     * every step P(x) is true -> ∀𝑥𝑃(𝑥) is true.
     * a step P(x) is false ->  ∀𝑥𝑃(𝑥) is false and the loop terminates.
     
<img width="596" alt="스크린샷 2022-09-11 오전 2 21 20" src="https://user-images.githubusercontent.com/63464299/189497103-0ad99e38-ec31-433f-97a1-82bffe889355.png">{: width="450" height="300"}

* ∃𝑥𝑃(𝑥) loop
     * some step P(x) is true -> ∃𝑥𝑃(𝑥) is true and the loop terminates.
     * P(x) 결과값이 true가 없이 loop가 끝난다면 -> ∃𝑥𝑃(𝑥) is false.


<img width="602" alt="스크린샷 2022-09-11 오전 2 20 42" src="https://user-images.githubusercontent.com/63464299/189497108-dd7b52a7-7baa-44d6-9d59-de0a4c580961.png">{: width="450" height="300"}

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
De Morgan’s Laws for Quantifiers<br/>

|Negation|Equivalent Statement|
|:---:|:---:|
|¬∃xP(x)|∀x¬P&#40;x&#41;|
|¬∀xP(x)|∃x¬P&#40;x&#41;|

“Every student in your class has taken a course in C.” – ∀xC(x)<br/>
“It is not the case that every student in your class has taken C.” – ¬∀xC(x)<br/>
“There is a student in your class who has not taken C.” – ∃x¬C(x)<br/>

-----------------

# Nested Quantifiers(중첩 한정자)
∀x(∃y(x + y = 0))<br/>
한정자의 순서는 값에 영향을 미침<br>
* **∀x**(**∃y**(x + y = 0)): 모든 x에 대해 “x + y = 0”을 만족하는 y가 존재한다 -> **True**
* **∃y**(**∀x**(x + y = 0)): 어떤 y에 대해 모든 x가 “x + y = 0”을 만족하는 y가 존재한다 -> **False**

## Order of Quantifiers
순서 중요!<br/>
Ex) "x+y = y+x"<br/>
→ ∀x∀yP(x,y) ≡ ∀y∀xP(x,y)<br/>

Ex) "x+y = 0"<br/>
→ ∀x∃yQ(x,y) is true<br/>
→ ∃y∀xQ(x,y) is false

<br/>
L(x,y) = "x loves y"<br/>
Ex) "Everybody loves somebody"<br/>
→ ∀x∃yL(x,y)<br/>
Ex) "There is someone who is loved by everyone"<br/>
→ ∃y∀xL(x,y)<br/>
Ex) "There is someone who loves everyone"<br/>
→ ∃y∀xL(y,x)<br/>

-----------------

# Negating Nested Quantifiers
∀w¬∀a∃f(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a¬∃f(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a∀f¬(P(w, f) ∧ Q(f, a))<br>
  ≡ ∀w∃a∀f(¬P(w, f) ∨ ¬Q(f, a))<br>
