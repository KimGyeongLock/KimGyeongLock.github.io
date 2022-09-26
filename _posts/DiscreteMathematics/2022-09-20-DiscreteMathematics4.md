---
layout: single
title: Proofs (How to prove)
toc: true
toc_sticky: true
categories: Discrete
published: true
---


# Proving Theorems
## Trivial Proof (자명한 증명)
* q = True
* p→q = True
* “If it is raining the 1=1.”
* **결론이 항시 True**임을 증명

## Vacuous Proof (무의미한 증명)
* p = False
* p→q = True
* “If n is both odd and even, then 2 + 2 = 5”
* **가정이 False**임을 증명

## Direct Proof (직접 증명)
* **p가 True**라고 가정할 때 **q가 True**임을 증명
* using rules of inference, axioms, logical equivalences
* Ex1)<br/>
    “If n is an odd integer, the n^2 is odd”<br/>
    Assume that n is odd. n = 2k+1 (k: integer)<br/>
    n^2 = (2k+1)^2 = 4k^2+4k+1 = 2(2k^2+2k)+1 = 2r+1 (r = 2k^2+2k) : odd
* Ex2)<br/>
    the sum of two rational numbers is rational<br/>
    Assume r and s are two rational numbers.<br/>
    <img width="179" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191149842-248f15c6-307a-4f69-913b-4bf70593fcc5.png"><br/><br/>
    <img width="146" alt="pu + qt" src="https://user-images.githubusercontent.com/63464299/191149865-e863b272-b10c-4f11-8762-e9b386ec9b43.png"><br/>
    the sum is rational

## Proof by Contraposition (대우에 의한 증명)
* **¬q가 True**라고 가정할 때 **¬p가 True**임을 증명
* **Indirect proof** (간접 증명)
* Ex1)<br/>
    “If n is an integer and 3n+2 is odd, then n is odd.”<br/>
    ¬q: n is even, n = 2k<br/>
    3n+2 = 3(2k) + 2 = 6k + 2 = 2(3k+1) : even,  ∴¬q → ¬p<br/>
    => p → q 
* Ex2)<br/>
    “If n^2 is odd, the n is odd(n: integer)”<br/>
    ¬q: n is even, n = 2k<br/>
    n^2 = 4k^2 = 2(2k^2) : even,  ∴¬q → ¬p<br/>
    => p → q

## Proof by Contradiction (모순에 의한 증명)
* 주어진 가정(p)을 부정(false)했을 때(**¬p**)<br/>
  항상 False가 되는 명제가 있음을 보이면(**¬p→F**)<br/>
  p의 가정이 잘못되었으므로 p는 True가 됨(**T→p**)
* Ex)<br/>
  “<img width="20" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191149959-698152c7-d217-4459-93a9-61a645955167.png">is irrational”<br/>
  ¬p: <img width="20" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191149982-9736cc84-da53-42b3-ae4b-7a3f365d3205.png">is rational 
  <img width="20" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191149982-9736cc84-da53-42b3-ae4b-7a3f365d3205.png">= a/b (b≠0, a and b have no common factors)<br/>
  <img width="41" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191150104-e4ac5816-f6ff-4b47-bea7-9f53e40a933a.png"><br/>
  <img width="57" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191150136-55c0108c-af83-4904-9b18-987d31f26e3c.png"><br/>
  a^2: even → a: even, a=2c(c: integer)<br/>
  <img width="146" alt="2b2 = a = (2c)2 = 4c2" src="https://user-images.githubusercontent.com/63464299/191150177-5bda1aff-cc56-451a-adbc-b288c060769c.png"><br/>
  <img width="56" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191150199-ecc1c7a5-64e6-4124-bb41-9cf3e4f2714e.png"><br/>
  b^2: even → b: even<br/>
  **This contradicts our assumption that a and b have no common factors.(even 2)**<br/>
  ¬p → F => T → p

## Theorems that are Biconditional Statements
* p → q and q →p are both true임을 증명
* Ex)<br/>
    “n is odd **iff** n^2 is odd when n is an integer.”

----------

# Proof Methods and Strategy
## Proof by Cases (사례에 의한 증명)
* 각각의 (pi → q)를 증명함으로써 전체를 증명하는 방법<br/>
<img width="138" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191174579-6cddefda-086c-4145-9d00-85e5c09ac60a.png"><br/>
위 conditional statement를 증명하기 위해 아래 tautology를 사용<br/>
<img width="142" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191174600-273868d4-b04a-4685-90be-035804b9b632.png"><br/>
<img width="193" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191174623-43a5bf6b-6c28-420f-a3ad-d040ff98a06e.png">


## Existence Proofs (존재 증명)
* ∃xP(x) 형태의 theorems 증명
* Constructive(생산적 존재 증명)
    * P(c)를 true로 하는 하나 이상의 c를 찾아 증명하는 방법 (Existential Generalization(EG))
    * Ex)<br/>
	<img width="132" alt="- b3 = c3 + d3" src="https://user-images.githubusercontent.com/63464299/191174641-ed48e7a5-67bf-4957-9f1a-014399388c95.png">
<br/>
	**\<one example\>** 1729 = 10^3 + 9^3 = 12^3 + 1^3
* Nonconstructive(비생산적 존재 증명)
    * P(c)를 true로 하는 값이 존재하지 않는다고 가정하고 모순을 도출하여 존재를 증명하는 방법
    * Ex)<br/>
      There exist irrational numbers x and y such that x^y is rational<br/>
      ¬p: There is no irrational numbers x and y such that x^y is rational -> x^y must be irrational<br/>
      x^y, x are irrational -> <img width="32" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191174774-0a7c458b-6442-47d6-8be2-a2d70d7f0259.png"> must be irrational<br/>
      **\<one counter example\>** <img width="235" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191174855-0c79b27c-409d-491c-bcc8-cee4a9dacce7.png"><br/>
	∴ ¬p is wrong, p is proved

## Counterexamples
* ∃x¬P(x) ≡ ¬∀xP(x) 
* ¬P(c) is true or P(c) is false -> ¬∀xP(x) is true
* ‘c’: **counterexample**


## Uniqueness Proofs
* **∃!xP(x)** : “there exists a unique x satisfying P(x)” or “there is exactly one x such that P(x)”
* 증명과정
    * **Existence**(존재): 특성을 가진 element x의 존재를 증명
    * **Uniqueness**(유일성): y≠x이면 y는 특성을 갖지 않음을 증명
* Ex)<br/>
  “If a and b are real numbers and a≠0, there is a unique real number r such that ar+b=0”<br/>
  **Existence**: r=-b/a <- a(-b/a) + b = -b + b =0<br/>
  **Uniqueness**: s is a real number such that as + b = 0(**s≠r**)<br/>
  ar+b = 0 = as + b -> r =s (**contradiction**)<br/>
  **∴-b/a is the only real number for r such that ar + b =0**

## Proof Strategies
* Choose a method
    * First **Direct method**
    * 안되면 Second **Indirect method** ( or contrapositive…)
* Choose a strategy
    * First **Forward reasoning**
    * 안되면 Second **Backward reasoning**


## Universally Quantified Assertions
* ∀xP(x) 형태의 theorems 증명
* x is an arbitrary member of the domain -> P(x) must be true(Universal Generalization(UG))
* Ex)<br/>
  “An integer x is even if and only if x^2 is even”<br/>
  p ↔︎ q ≡ (p→q)∧(q→p)<br/>
  case 1: (p→q) If x is even x=2k, x^2 = 4k^2 = 2(2k^2) : even<br/>
  case 2: (q→p)=>(¬p→¬q)\<contraposition\><br/>
  Assume x is not even then x^2 is not even -> x is odd and x^2 is odd<br/>
  x = 2k+1, x^2 = (2k+1)^2 = 4k^2+4k+1 = 2(2k^2+2k)+1 : odd



