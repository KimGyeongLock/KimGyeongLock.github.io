---
layout: single
title: Recursion2
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Structural Induction (구조적 유도)

* recursively defined set의 elements 속성을 증명하기 위해 사용
* Basic Step
	– Show that the result holds for all elements specified in the basis step of the recursive definition. 
* Recursive Step
    * Show that if the statement is true for each of the elements used to construct new elements in the recursive step of the definition, the result holds for these new elements. 

## Full Binary Trees Examples
* full binary tree T의 높이 h(T)
    * Basis Step
        * root r의 h(T) = 0
    * Recursive Step
        * T1, T2: full binary trees ->
        * T = T1∙T2 
        * h(T) = 1 + max(h(T1), h(T2))
* full binary tree vertices의 갯수 n(T)
    * Basis Step
        * root r의 n(T) = 1
    * Recursive Step
        * T1, T2: full binary trees ->
        * T = T1∙T2 
        * n(T) = 1 + n(T1) + n(T2)
* T: full binary tree, -> n(T) ≤ 2^(h(T)+1) -1
    * Basis Step
        * a full binary tree consisting only of a root
        * n(T) = 1 & h(T) = 0
        * n(T) = 1 ≤ 2^(0+1) - 1 = 1
    * Recursive Step
        * Assume n(T1) ≤ 2^(h(T1)+1) - 1 and n(T2) ≤ 2^(h(T2)+1) - 1
        * n(T) = 1 + n(T1) + n(T2) ≤ 1 + (2^(h(T1)+1) - 1) + (2^h(T2)+1 - 1) ≤ 2*max(2^(h(T1)+1), 2^(h(T2)+1)) - 1 = 2*2^(max(h(T1), h(T2))+1) - 1 =2*2^h(T) - 1 =2^(h(T)+1) - 1

--------------

# Generalized Induction
* **Lexicographic ordering**
    * (x1, y1) ≤ (x2, y2) 
      * if either (x1 < x2) or (x1=x2 and y1 < y2)


# Recursive Algorithms
* Recursive algorithm
    * smaller input으로 문제의 instances를 줄여 문제 해결
    * instances는 initial case까지 줄임
* Ex) factorial n
    * procedure factorial(n: nonnegative integer)
	if n = 0 then return 1
	else return n\*factorial(n-1)
	\{output is n!\}
* recursive algorithm의 정확성 증명 방법
    * **mathematical induction**
    * **strong induction**
* **Merge Sort**


