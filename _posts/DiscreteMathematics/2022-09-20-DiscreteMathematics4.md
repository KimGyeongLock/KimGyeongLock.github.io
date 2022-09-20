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
* 결론이 항시 True임을 증명

## Vacuous Proof (무의미한 증명)
* p = False
* p→q = True
* “If n is both odd and even, then 2 + 2 = 5”
* 가정이 False임을 증명

## Direct Proof (직접 증명)
* p가 True라고 가정할 때 q가 True임을 증명
* using rules of inference, axioms, logical equivalences
* Ex1)<br/>
    “If n is an odd integer, the n^2 is odd”<br/>
    Assume that n is odd. n = 2k+1 (k: integer)<br/>
    n^2 = (2k+1)^2 = 4k^2+4k+1 = 2(2k^2+2k)+1 = 2r+1 (r = 2k^2+2k)
	•	Ex2)<br/>
    the sum of two rational numbers is rational<br/>
    Assume r and s are two rational numbers.<br/>
    <img width="179" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191149842-248f15c6-307a-4f69-913b-4bf70593fcc5.png"><br/>
    <img width="146" alt="pu + qt" src="https://user-images.githubusercontent.com/63464299/191149865-e863b272-b10c-4f11-8762-e9b386ec9b43.png"><br/>
    the sum is rational

## Proof by Contraposition (대우에 의한 증명)
* Assume ¬q and ¬p가 true임을 증명
* **Indirect proof** (간접 증명)
* Ex1)<br/>
    “If n is an integer and 3n+2 is odd, then n is odd.”<br/>
    ¬q: n is even, n = 2k<br/>
    3n+2 = 3(2k) + 2 = 6k + 2 = 2(3k+1) : even,  ∴¬q → ¬p<br/>
    => p → q 
	•	Ex2)<br/>
    “If n^2 is odd, the n is odd(n: integer)”<br/>
    ¬q: n is even, n = 2k<br/>
    n^2 = 4k^2 = 2(2k^2) : even,  ∴¬q → ¬p<br/>
    => p → q

## Proof by Contradiction (모순에 의한 증명)
* 주어진 가정(p)을 부정(false)했을 때(¬p)<br/>
  항상 False가 되는 명제 q가 있음을 보이면(¬p→F)<br/>
  p의 가정이 잘못되었으므로 p는 True가 됨(T→p)
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
  **This contradicts our assumption that a and b have no common factors.(even 2)**

## Theorems that are Biconditional Statements
* p → q and q →p are both true임을 증명
* Ex)<br/>
    “n is odd iff n^2 is odd when n is an integer.”

----------

# Proof Methods and Strategy
## Proof by Cases

## Existence Proofs
* Constructive
* Nonconstructive

## Counterexamples

## Uniqueness Proofs

## Proof Strategies

## Universally Quantified Assertions


