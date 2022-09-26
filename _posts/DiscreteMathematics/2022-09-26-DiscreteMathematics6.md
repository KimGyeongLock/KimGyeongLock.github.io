---
layout: single
title: Functions and Sequances
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Functions
= **mappings** or **transformations**<br/>
<br/>
**f: A → B**: function f from A to B
* A의 각 element는 B의 오직 한 element만 가짐
* f(a) = b
    * b: **image** of a
    * a: **preimage** of b
* AxB(cartesian product)의 subset(relation)으로 정의 가능
    * But! 같은 첫번째 element를 가질 수 없음!
        * (a, b), (a, d) (X)
* A: **domain**
* B: **codomain**
* range of f: the set of **all images** of points in A = subset of codomain
* A=B ↔︎
    * same domain
    * same codomain
    * f(a)=f(b)=x


## Injections (단사함수, 일대일 함수)
* **one-to-one** or **injective** ↔︎
* f(a) = f(b) → a = b
    * Not Injective<br/>
      f(a) = z<br/>
      f(c) = z<br/>
      f(a) = f(c)<br/>
      a ≠ c

## Surjections (전사 함수)
* **onto** or **surjective** ↔︎
* ∀b(∃a(f(a)=b)) (b∈B, a∈A)
* 모두 짝이 맞을 때
    * Not surjective<br/>
      f(?) = v

## Bijections (전단사 함수, 일대일 대응)
* **one-to-one correspondence** or **bijection**
* both one-to-one and onto (injective and surjective)

----------

# Showing that F is one-to-one or onto
* To show that f is injective
    * f(x) = f(y) → x = y
* To show that f is not injective
    * f(x) = f(y) ∩ x ≠ y
* To show that f is surjective
    * f(x) = y 
* To show that f is not surjective
    * f(x) ≠ y

----------

# Inverse functions
* A, B: bijection →  <img width="38" alt="스크린샷 2022-09-26 오후 7 54 49" src="https://user-images.githubusercontent.com/63464299/192265280-3c677964-621e-48ec-8964-2e74ac5f67f7.png"> (**inverse** of f)
    * f가 bijection이 아니면 No Inverse
    * <img width="207" alt="스크린샷 2022-09-26 오후 7 57 48" src="https://user-images.githubusercontent.com/63464299/192265316-f8f54a34-d4fc-480c-97c8-2749a9987ac6.png">

----------

# Composition
* f ￮ g : the composition of f with g
    * f ￮ g(x) = f(g(x))

----------

# Some Important Functions
* The **floor** function (내림)
    * f(x) = **⎣x⎦**
    * x보다 작거나 같은 integer 중 가장 큰 integer
* The **ceiling** function (올림)
    * f(x) = **⎡x⎤**
    * x보다 크거나 같은 integer 중 가장 작은 integer
    
## Exercise
x is a real number → ⎣2x⎦ = ⎣x⎦ + ⎣x + 1/2⎦
* Sol)<br/>
  x =  n + 𝜀 (n: integer, 0 ≤ 𝜀 < 1)
    * Case 1: 𝜀 < 1/2
        * ⎣2x⎦ =⎣2n + 2𝜀⎦ = 2n
        * ⎣x + 1/2⎦ = ⎣n + 𝜀 + 1/2 ⎦ = n
        * ⎣2x⎦= 2n , ⎣x⎦+⎣x + 1/2⎦ = 2n
    * Case 2: 𝜀 ≥ 1/2
        * ⎣2x⎦ =⎣2n + 2𝜀⎦ = 2n + 1
        * ⎣x + 1/2⎦ = ⎣n + 𝜀 + 1/2 ⎦ = n + 1
        * ⎣2x⎦= 2n+1 , ⎣x⎦+⎣x + 1/2⎦ = n + (n+1) = 2n+1

----------

# Factorial Function
* f(n) = n!
* 1부터 n까지 양의 정수의 곱 (n: nonnegative number)
* f(n) = 1•2 ••• (n-1) • n, f(0) = 0! = 1
* Stirling’s Formula<br/>
  <img width="300" alt="스크린샷 2022-09-26 오후 8 24 24" src="https://user-images.githubusercontent.com/63464299/192265357-303a61c4-387f-4324-b857-7f9f7d8ff02d.png">
  
