---
layout: single
title: Counting
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Product Rule
* **n1 * n2**
* Counting Functions
    * m elements in the domain
    * n elements in the codomain
    * **n^m**
* Counting One-to-One Functions
    * n(n−1) (n−2)∙∙∙(n−m +1)
    * = **n! / (n-m)!**
* Counting Subsets of a Finite Set
    * **2^\|S\|** 
* Product Rule in Terms of Sets
    * element in the Cartesian product A1 ⨉ A2 ⨉ ∙∙∙ ⨉ Am
    * \|𝐴1 ×𝐴2 ×⋯×𝐴m\|=\|𝐴1\|∙\|𝐴2\|∙⋯∙\|𝐴m\|

--------------

# Sum Rule
* **n1 + n2**
* Sum Rule in terms of sets
    * \|𝐴1 ∪ 𝐴2 ∪ ⋯ ∪ 𝐴m\| = \|𝐴1\| + \|𝐴2\|+ ⋯ + \|𝐴m\| (𝐴i ∩ 𝐴j = ∅ for all i, j)
* Combining the sum and product rule 
    * sum rule + product rule

--------------

# Subtraction Rule
* Principle of inclusion - exclusion
    * **\|𝐴 ∪ 𝐵\| = \|𝐴\| + \|𝐵\| − \|𝐴 ∩ 𝐵\| **

--------------

# Division Rule
* **n / d**
* Ex) How many ways are there to seat four people around a circular table, where two seatings are considered the same when each person has the same left and right neighbor? 
    * n = 24
    * d = 4 (same situation)
    * 24 / 4 = 6
