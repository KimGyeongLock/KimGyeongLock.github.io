---
layout: single
title: Recursion
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Recursively Defined Functions
* A **recursive** or **inductive** definition of a function
* two steps
    * **Basis Step: f(0)**
    * **Recursive Step**: 
        * 더 작은 integers(k-1, k-2)로 integer(k)의 값을 찾는 규칙 제공
* Ex)
    * Basis Step: f(0) = 3
    * Recursive Step: f(n+1) = 2f(n) +3
    * **Fibonacci Numbers**
        * Basis Step: f0 = 0, f1 = 1
        * Recursive Step: fn = fn-1 + fn-2 for n>=2

--------------

# Recursively Defined Sets
* **Basis Step: initial collection ∈ S**
* **Recursive Step:**
    * 이미 집합에 있는 것으로 알려진 요소로부터 집합에 새로운 요소를 형성하는 규칙 제공
* Ex)
    * Basis Step: 3 ∈ S
    * Recursive Step: 
        * x∊S ∧ y∊S → x+y ∈S 
* **Strings**
    * **Σ: Set of symbols**
    * **Σ*: Set of strings**
    * Basis Step: λ ∊ Σ* (λ = empty string)
    *  Recursive Step: 
        * w ∈ Σ* ∧ x ∈ Σ → wx ∈ Σ*
    * Ex)
        * Σ = {0,1}
        * Σ* = {λ,0,1, 00,01,10, 11…} 

--------------

# Recursively Defined Sets and Structures
* **String Concatenation(∙)**
    * Basis Step: w ∈ Σ* → w∙λ = w
    * Recursive Step:
        * (w1 ∈ Σ*  ∧ w2 ∈ Σ*  ∧ x ∈ Σ) → w1 ∙(w2x) = (w1∙w2)x 
* **Length of a String**
    * l(w): the length of string w
    * Basis Step: 𝑙(𝜆) = 0
    * Recursive Step: 𝑤 ∈ ∑∗ ∧ 𝑥 ∈ ∑ → 𝑙(𝑤𝑥) = 𝑙(𝑤) +1
* **Well-Formed Formula in Propositional Logic**
    * Basis Step: T, F, s(propositional variable): well-formed formula
    * Recursive Step:
        * E, F: well-formed formula → (¬ E), (E ∧ F), (E ∨ F), (E → F), (E ↔ F): well-formed formula
    * Ex)
        * ((p ∨q) → (q ∧ F)) well-formed formula임을 증명
        * Basis Step: T, F, p, q: well-formed formula
        * Recursive Step: 
            * (p ∨ q), (p → F), (F → q), (q ∧ F): well-formed formula
            * ((p ∨ q) → (q ∧ F)): well-formed formula

* **Rooted Trees**
    * a set of **vertices**
        * root(distinguished vertex)
    * **edges**
        * connecting vertices
    * Basis Step: r(single vertex) = rooted tree
    * Recursive Step: 
        * Suppose that T1, T2, … Tn are disjoint rooted trees with roots r1, r2, … rn respectively
        * root r 에서 각 vertices r1, r2,…rn에 edge를 추가 -> a new rooted tree
        * Set increased by using recursive step

* **Full Binary Trees**
    * 모든 노드가 0개(leaf case) 혹은 2개의 vertices을 가짐(specific case)
    * Basis Step: r(single vertex) = rooted tree
    * Recursive Step: 
        * Suppose that T1, T2 are disjoint full binary trees.
        * 왼쪽 subtree T1과 오른쪽 subtree T2의 각 roots에 루트 r을 연결하는 edge + 루트 r -> full binary tree

* **Induction and Recursively Defined Sets**
    * mathematical induction 사용하여 recursively defined sets에 대하 결과를 증명



