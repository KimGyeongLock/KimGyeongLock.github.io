---
layout: single
title: \[예습] Propositional Logic
toc: true
toc_sticky: true
categories: Discrete
published: true
---

**Logic** (Logic System)
* **Syntax(구조)**: symbolic structure of the statements
* **Semantics(의미)**: a mapping from symbolic structures to things that the logic system concerns

# Propositional Logic
Proposition(명제): declarative sentence **(Only True or False)**
-  1+1=2 (T)
-  Toronto is the capital of Canada (F)
-  ~~1 + 2 + 3~~
-  ~~x + 1 = 2~~

**Positional Variable**: a symbol that represents a propositional
statement
- p, q, r, s⋅⋅⋅

**Atomic Proposition**: one that cannot be expressed in term of simpler terms
- **T**: True
- **F**: False

**Compound Proposition**: one or more propositions + logical operators
- **Logical Operator**
  - **Negation**(NOT)
    - ¬p
    - |p|¬p|
      |:---:|:---:|
      |T|F|
      |F|T|
  
  - **Conjunction**(AND)
    - p ∧ q
    - |p|q|p ∧ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|F|
  - **Disjunction**(OR)
    - p ∨ q
    - |p|q|p ∨ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Exclusive-Or**(XOR)
    - p ⊕ q
    - |p|q|p ⊕ q|
      |:---:|:---:||:---:|
      |T|T|F|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Implication**(IMPLIES)
    - (Conditional Statement) 
    - p → q = ¬p ∨ q
    - |p|q|p → q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|T|
      |F|F|T| 
    - p(가설)가 거짓이면 q(결론)를 판단 할 수 없기 때문에 True
    - q는 p의 필요조건 
    - p는 q의 충분조건
    - **Converse**(역): q → p
    - **Inverse**(이): ¬p → ¬q
    - **Contrapositive**(대우): ¬q → ¬p
  - **Biconditional**(IFF)
    - p ↔ q
    - |p|q|p ↔ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|T|
    
    - 필요 충분 조건
      
* Equivalence<br/>
![propositional+logic](https://user-images.githubusercontent.com/63464299/183473997-f5504f2a-f873-4377-bd89-c77699ad6086.jpg)<br/>
De Morgan's law: ¬p ∧ q ↔ ¬p ∨ ¬q, ¬p ∨ q ↔ ¬p ∧ ¬q
 
 
# Propositional Satisfiability
* **Satisfiable** Proposition: propositional variable에 하나라도 true를 넣었을때 결과로 True가 나오는 것
* **Unsatisfiable** Proposition: Not Satisfiable -> **Contradiction**
* **Valid** Proposition: 모든 결과가 True -> **Tautology**
  
