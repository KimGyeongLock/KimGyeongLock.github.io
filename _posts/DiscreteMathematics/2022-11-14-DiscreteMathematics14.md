---
layout: single
title: Counting3
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Binomial Coefficients and Identities
* Powers Binomial Expression
    * binomial expression: sum of two terms(x+y)
    * (x+y)^n
<img width="592" alt="스크린샷 2022-11-14 오후 9 07 54" src="https://user-images.githubusercontent.com/63464299/201667163-f0564baf-547d-43c6-a41e-bb1364246e95.png">

    * ∑C(n, k) = 2^n
* Pascal’s Identity
    * n≥k≥0 
    * C(n+1, k) = C(n, k-1) + C(n, k)
    * Pascal’s Triangle

------------

# Generalized Permutations and Combinations
* **Permutations with repetition**(중복순열)
    * **n^r**
* **Combinations with repetition**(중복조합)
    * **C(n+r-1, r) = C(n+r-1, n-1)**
* Permutations with **Indistinguishable** objects
    * **n! / 𝑛1!𝑛2!⋯𝑛k!**

## Distributing Objects into Boxes
* **Distinguishable** objects and **distinguishable** boxes
    * **n! / 𝑛1!𝑛2!⋯𝑛k!**
* **Indistinguishable** objects and **distinguishable** boxes
    * **C(n+r-1, r)**
* **Distinguishable** objects and **Indistinguishable** boxes
    * no simple closed formula
    * **집합의 분할 S(4, 3)**
        * 4 = C(4,4) = 1
        * 1 3 = C(4,1)*C(3,3) = 4
        * 2 2 = C(4,2)*C(2,2)/2! = 3
        * 1 1 2 = C(4,1)*C(3,1)*C(2,2)/2! = 6
* **Indistinguishable** objects and **Indistinguishable** boxes
    * no simple closed formula
    * **자연수의 분할 P(6, 4)**
        * 6, (5,1), (4,2), (4,1,1), (3,3), (3,2,1), (3,1,1,1), (2,2,2), (2,2,1,1)
