---
layout: single
title: Counting2
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# The Pigeonhole Principle (비둘기집의 원리)
* k+1개의 objects를 k개의 상자에 넣으려면, 적어도 한 상자는 두개 이상이 들어가야한다.
* p: k+1 obejcts are placed into k boxes
* q: at least one box contains two or more objects
* Proof
    * contraposition
        * ¬q→¬p: none of the k boxes has more than one object
        * -> object의 최대갯수 = k ≠ k+1 (contradiction) 

## Generalized Pigeonhole Principle
* N개의 objects를 k개의 상자에 넣으려면, 적어도 한 박스는 적어도 **⎡N/k⎤**개의 objects를 포함
* p: N objects are placed into k boxes 
* q: at least one box containing at least ⌈N/k⌉ objects 
* Proof
    * contraposition
        * ¬q→¬p: none of the boxes contains more than ⌈N/k⌉ − 1 objects 
        * N/k ≤ ⎡N/k⎤- 1 => N ≤ k(⎡N/k⎤- 1 ) < k((N/k+1) - 1) = N (contradiction)

----------

# Permutations (순열)
* **ordered** arrangement
* **r-permutation**: An ordered arrangement of r elements of a set
* **P(n,r)**: The number of r-permutations of a set with n elements
    * P(n,r) = n(n-1)(n-2)∙∙∙ (n−r+1) = **n! / (n-r)!**

----------

# Combinations (조합)
* **unordered** selection of r elements
* **r-combination**: a subset of the set with r elements
* **C(n,r)**: The number of r-combinations of a set with n distinct elements
    * C(n,r) = **n! / (n-r)!r!** = P(n,r) / r!
    * C(n,r) = **C(n, n-r)**
