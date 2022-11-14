---
layout: single
title: Discrete Probability
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Introduction to Discrete Probability
* Key Terms
    * experiment
        * a procedure that yields one of a given set of possible outcomes
        * Ex) rolling a dice
    * **sample space**
        * the set of possible outcomes
        * Ex) {1, 2, 3, 4, 5 ,6}
    * **event**
        * a subset of the sample space
        * Ex) {2, 4, 6}
* Probability of an Event
    * S: a finite sample space of equally likely outcomes
    * E: an event
    * Probability of E: **P(E) = \|E\| / \|S\|**
    * 0≤ 𝑝(𝐸) ≤1
* Complements
    * **𝑝(𝐸-bar)=1−𝑝(𝐸)**
* Unions
    * **𝑝(𝐸1∪𝐸2) =𝑝(𝐸1) +𝑝(𝐸2) − 𝑝(𝐸1 ∩ 𝐸2)** 

------------

# Probability Theory
* **Probability distribution** (확률분포)
    * the function p from the set of all outcomes of the sample space S
    * 0≤ 𝑝(𝑠) ≤1 for each 𝑠∈𝑆
    * ∑𝑠∈𝑆 𝑝(𝑠) = 1 
* **Uniform Distribution** (항등분포)
    * 집합 S의 각 element의 확률 = 1/n
    * p(1) = p(2) = ∙∙∙ = p(n) = 1/n
* Probability of an Event
    * p(E) = ∑𝑠∈𝑆 𝑝(𝑠)
* Complements and Unions
    * 𝑝(𝐸-bar)=1−𝑝(𝐸) 
    * ∑s∈S 𝑝(𝑠) = 1 = 𝑝(𝐸) + 𝑝(𝐸-bar)
    * 𝑝(𝐸1∪𝐸2) =𝑝(𝐸1) +𝑝(𝐸2) − 𝑝(𝐸1 ∩ 𝐸2) 
* Combinations of Events
    * E1, E2, … is a sequence of pairwise disjoint events in a sample space S
    <img width="176" alt="스크린샷 2022-11-14 오후 11 15 46" src="https://user-images.githubusercontent.com/63464299/201692257-77b930f8-f4a4-4550-9b6c-87a24d882600.png">

* **Conditional Probability** (조건부 확률)
    * p(F) > 0
    * **p(E\|F) = 𝑝(𝐸∩𝐹)/p(F)**
* **Independence** (독립)
    * 𝑝(𝐸∩𝐹) = p(E)p(F) 
* Pairwise and Mutual Independence
    * pairwise independent
        * P(A∩B) = P(A)P(B)
        * P(A∩C) = P(A)P(C)
        * P(B∩C) = P(B)P(C)
    * mutually independent
        * P(A∩B∩C) = P(A)P(B)P(C)
        * P(A∩B) = P(A)P(B)
        * P(A∩C) = P(A)P(C)
        * P(B∩C) = P(B)P(C)
* **Bernoulli Trials**
    * only two possible outcomes(success and failure)
    * p: probability of success
    * q: probability of failure
    * p+q=1
* **Binomial distribution**
    * **b(k:n, p) = C(n,k)p^k*q^(n-k)**
