---
layout: single
title: Relations2
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Equivalence Relations
* **Equivalence Relation**
    * **reflexive, symmetric, transitive** 모두 만족하는 set A의 relation
    * Ex) aRb, 𝑎 ≡ 𝑏 (mod 𝑚) 
* Equivalent
    * equivalence relation과 관련된 a, b elements
    * a ~ b
* **Equivalence Classes**
    * R: set A에서 equivalence relation
    * set A의 element a와 관련된 모든 elements의 set
    * R에 대한 a의 equivalence class: \[a\]R
        * **[a]R = {s\|(a, s) ∈ R}**
    * **b ∈ \[a\]R**
        * b: **representative** of equivalence class
        * = aRb
    * Ex) equivalence classes of the relation congruence modulo = congruence classes modulo
        * {s \| (a, s) ∈ modulo m} = a ≡ s (mod m)
* Theorem 1
    * **aRb = \[a\]=\[b\] = \[a\] ∩ \[b\] ≠ 𝜙**
* **Partition** of a Set
    * a collection of disjoint nonempty subsets of S
    * the collection of subsets Ai, where i ∈ I
        * 𝐴𝑖 ≠ ∅ for 𝑖 ∈ 𝐼
        * 𝐴𝑖 ∩ 𝐴𝑗 = ∅ when 𝑖 ≠ 𝑗 
        * ⋃i∈I 𝐴i =𝑆 
    * R(equivalence relation)의 모든 equivalence classes의 union = all of A
    * ⋃a∈A \[𝑎\]R = 𝐴 
    * equivalence classes = equal or disjoint
        * [a]R ∩ [𝑏]R = ∅ when [𝑎]R ≠ [𝑏]R 
        * the equivalence classes form a partition of 𝐴 

-----------

# Partial Ordering
* **Partial Orderings**
    * **reflexive, antisymmetric, transitive**를 만족하는 set S의 relation
    * partially ordered set or poset
        * a set together with a partial ordering R
        * (S, R)
        * Ex) (Z+, ≥), (Z+, \|)
    * Members of S = elements of the poset
* **Comparability**
    * either 𝑎≼𝑏 or 𝑏≼𝑎 → poset(𝑆,≼)의 elements a,b = **comparable** 
    * neither 𝑎≼𝑏 nor 𝑏≼𝑎 → poset(𝑆,≼)의 elements a,b = **incomparable** 
* **Total order** & **Totally ordered set**
    * Totally ordered(linearly ordered set)
        * **(𝑆, ≼)**: poset ∧ every two elements of S: comparable 
    * Total order(linear order)
        * **≼**
    * Totally ordered set = chain
* **Well-ordered set**
    * ≼: a total ordering ∧ every nonempty subset of 𝑆 has a least element. 
* **Lexicographic Order** (사전식 정렬)
    * (a1,a2) ≺ (b1, b2)
    * Ex)<br/>discreet ≺ discrete<br/>discreet ≺ discreetness 
* **Hasse Diagrams**
    * reflexive and transitive properties를 보여주는 edges를 제거한 partial ordering 표현방법
    1. reflexive property로 인해 모든 vertex에 존재하는 Loop 제거
    2. Remove all edges(𝑥,𝑦) for which there is an element 𝑧∈𝑆 such that 𝑥≺𝑧 and 𝑧≺𝑦. These are the edges that must be present due to the transitive property.
    3. initial vertex가 terminal vertex보다 아래 있도록 정렬
    4. 화살표 제거 because all edges point upwards toward their terminal vertex
