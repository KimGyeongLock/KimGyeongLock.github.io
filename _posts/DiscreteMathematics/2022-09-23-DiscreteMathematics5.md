---
layout: single
title: Sets
toc: true
toc_sticky: true
categories: Discrete
published: true
---

 
# Introduction
* **Set**: **unordered** collection of objects
* The objects in a set: **elements** or **members**
* **a∈A**: a is an element of the set A
* **a∉A**: a is not a member of A 

--------

# Describing a Set
* **S={a,b,c,d}**
    * 순서는 중요하지 않음
        * S = \{a,b,c,d\} = \{b,c,a,d\}
    * 같은 원소를 한번이상 나열해도 집합은 변하지 않음
        * S = \{a,b,c,d\} = \{a,b,c,b,c,d\}
    * Elipses (…): 생략
        * S = \{a,b,c,d,…..,z\}
* Some Important Sets
    * **N** = natural numbers = \{0,1,2,3,…\}
    * **Z** = integers = \{…, -3, -2, -1, 0, 1, 2, 3...\}
    * **Z+** = positive integers = \{ 1, 2, 3…\}
    * **R** = set of real numbers
    * **R+** = set of positive real numbers
    * **C** = set of complex numbers
    * **Q** = set of rational numbers 
* **Set-Builder Notation**
    * Specify the property(ies) (description)
        * S = \{ x \| x is a positive integer less than 100\}
        * O = \{ x \| x is an odd positive integer less than 10\}
        * O = \{ x∈Z+ \| x is odd and x<10\}
* **Interval Notation**
    * closed interval \[a,b\]
    * open interval (a, b)
        * [a,b] = \{ x \| a ≤ x ≤ b \}
        * [a,b) = \{ x \| a ≤ x < b \}
        * (a,b] = \{ x \| a < x ≤ b \}
        * (a,b) = \{ x \| a < x < b \}
* Sets can be elements of sets
    * \{\{1,2,3\}, a, \{b/c\}\}
    * {N,Z,Q,R}

-----------

# Universal Set and Empty Set
* **Universal Set (U)**
    * the set containing everything 
* **Empty Set (∅ or \{\})**
    * the set with no elements
    * **The empty set is different from a set containing the empty set**
       * ∅(empty set) ≠ \{∅\}(a set containing the empty set)
       
-----------

# Subsets(부분집합)
* **The set A is a subset of B**, **iff** every element of A is also an element of B
    * **A⊆B** ↔︎ ∀x(x∈A → x∈B)
    * IF) ∀x(x∈A ∧ x∉B), A cannot be a subset of B
* Showing that A is a Subset of B
    * if x belongs to A, then x also belongs to B
* Showing that A is not a Subset of B
    * find an element x ∈ A with x ∉ B (**counterexample**)
    * Ex)<br/>
      The set of integers with squares less than 100 is not a subset of the set of nonnegative integers<br/>
      counterexample: -1, -4 …

-----------

# Set Equality
* Two sets are equal **iff** they have the same elements
    * A, B: Sets, A=B ↔︎ ∀(x∈A ↔︎ x∈B)
    * Ex)<br/>
      {1,3,5} = {3,5,1}<br/>
      {1,5,5,5,3,3,1} = {1,3,5}

* **Logical equivalences**
    * A↔︎B ≡ (A→B) ∧ (B→A)
    * ∀x[(x∈A → x∈B) ∧ (x∈B → x∈A)]
    * ≡ A⊆B and B⊆A
* ∴A=B iff A⊆B and B⊆A

-----------

#  Proper Subsets(진부분집합)
* A is a subset of B & A에 속하지 않는 B의 원소가 적어도 하나 존재하는 경우
* A⊆B **but A≠B => A⊂B
* ∀x(x∈A → x∈B) ∧ ∃x(x∈B ∧ x∉A)

-----------

# Set Cardinality
The Cardinality of a finite set A
* the number of (distinct) elements in a set (**\|A\|**)
* Ex)
    * \|∅\| = 0
    * \|{(∅}\| = 1
    * \|{1,2,3}\| = 3

-----------

# Tuples
* The ordered elements n-tuple (a1,a2…an)
* 2-tuples: **ordered pairs**
* (a,b) = (c,d) ↔︎ a=c, b=d

-----------

# Cartesian Product(곱집합)
* A × B = {(a,b) \| a∈A ∧ b∈B}
* Ex)<br/>
    * A = {a,b} B = {1,2,3} C = {c, d}
    * A × B = {(a,1),(a,2),(a,3),(b,1),(b,2),(b,3)}
    * A × B × C = {(a, 1, c), (a, 1, d), (a, 2, c), … , (b,3,c), (b,3,d)}
        * \|A × B × C\| = 12

-----------

# Relation
* A subset R of the Cartesian Product(A × B)
* R⊆(AxB)
    * R = {(a,3),(b,1),(b,2)}

-----------

# Truth Sets of Quantifiers
The **truth set** of P
* the set of elements in D for which P(x) is true. 
* {x ∈ D \| P(x)}
* Ex)
    * domain: integers and P(x) = “\|x\|=1”
    * truth set of P(x) = {-1,1}

-----------

# Set Operations
* **Union**
    * A ∪ B
    * {x \| x∈A ∨ x∈B}
* **Intersection**
    * A ∩ B
    * {x \| x∈A ∧ x∈B}
    * intersection is empty(∅) -> **disjoint**
        * is not independent (컨셉이 다름)
* **Complement**
    * Ā  or A^c
    * {x∈U \| x∉A}  : U-A
* **Difference**
    * A - B 
    * {x \| x∈A ∧ x∉B}
* The Cardinality(\|\|) of the Union of Two Sets
    * \|A ∪ B\| = \|A\| + \|B\| - \|A ∩ B\|

-----------

# Set Identities
* Identity laws
    * A ∪ ∅ = A
    * A ∩ U = A
* Domination laws
    * A ∪ U = U
    * A ∩ ∅ = ∅
* Idempotent laws
    * A ∪ A = A
    * A ∩ A = A
* Complementation law
    * (Ẫ) = A
* Commutative laws
    * A ∪ B = B ∪ A
    * A ∩ B = B ∩ A
* Associative laws
    * A ∪ (B ∪ C) = (A ∪ B) ∪ C
    * A ∩ (B ∩ C) = (A ∩ B) ∩ C
* Distributive laws
    * A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)
    * A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)
* Absorption laws
    * A ∪ (A ∩ B) = A
    * A ∩ (A ∪ B) = A
* Complement laws
    * A ∪ Ā = U
    * A ∩ Ā = ∅
* De Morgan’s laws
  <img width="85" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191895849-784b7c71-acf0-4a05-b6da-ea7fc5df9d2f.png"><br/>
  <img width="85" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191895857-51c92435-a20c-4cd7-a76c-9a2c68cd651a.png">

-----------

# Proving Set Identities
3 ways to prove set identities
1. 각각의 set가 다른 set의 subset(⊆)임을 증명 
2. set builder notation, propositional logic 사용
3. Membership Tables


## Step1. Proof of Second De Morgan Law
<img width="85" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191895873-6c52b502-0c2d-43f9-9cc6-4a11fe47198e.png"><br/>
=> A=B iff A⊆B and B⊆A

1. <img width="88" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191895889-e3bae247-da2b-4109-b54e-a28f2c9a73d7.png">
   <br/>
   <img width="532" alt="스크린샷 2022-09-23 오후 1 59 58" src="https://user-images.githubusercontent.com/63464299/191895956-8c9b2810-99e8-439d-ac57-3e0896cd5de2.png">


2. <img width="88" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/191895912-abf0733b-333d-4cb0-812a-37a641bf680a.png">
   <br/> 
   <img width="592" alt="스크린샷 2022-09-23 오후 2 02 59" src="https://user-images.githubusercontent.com/63464299/191895969-56463ae2-3ac3-45a4-8143-d05e8b7adb87.png">

## Step 2. Set-Builder Notation: Second De Morgan Law

<img width="519" alt="스크린샷 2022-09-24 오후 11 57 32" src="https://user-images.githubusercontent.com/63464299/192104807-634aa31b-37ff-45a2-9379-b671017d09b2.png">

