---
layout: single
title: Sequences
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Introduction
* Sequences
    * ordered lists of elements
* Sequence(수열)
    * function from a subset of the integers to a set S
* Term(항) of the Sequence
    * <img width="14" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193302416-7a1ddd94-4842-4ad2-abae-6dec56a2680e.png">
    * denoting the image of the integer 𝑛

-----------

# Geometric Progression(등비수열)
<img width="100" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193302482-b5bf9226-76ac-4720-b100-6183954fb26b.png">
* a: initial term (초항)
* r: common ratio (공비)
* a&&r: real numbers

-----------

# Arithmetic Progression(등차수열)
<img width="177" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193302522-34dd0d29-6e47-4e10-9268-7749378b58d9.png">
* a: initial term (초항)
* d: common difference (공차)
* a&&d: real numbers

-----------

# Recurrence Relations(점화식)
* an equation that expresses an in terms of one or more of the previous terms of the sequence

-----------

## Solving Recurrence Relations
* Finding a **closed formula** for the **nth term** of sequence
* Method 1: **Working upward**
    * forward substitution
    * a2 -> a3 -> a4 -> … -> an = solution
* Method 2: **Working downward**
    * backward substitution
    * an = an-1 + d = (an-2 +d) +d … = a1 + d(n-1)

-----------

# Fibonacci Sequence
* Initial Conditions: <img width="90" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193302555-d9e514fe-76ce-4f37-917e-b21bc3a99b9e.png">

*  Recurrence Relation: <img width="90" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193302579-6e145e8b-aef0-487d-8efe-689ebfb96db3.png">
