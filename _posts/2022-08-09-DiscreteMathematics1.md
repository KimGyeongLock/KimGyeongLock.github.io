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
    - ¬𝑝<br/>
      |p|¬𝑝|
      |:---:|:---:|
      |T|F|
      |F|T|
  
  - **Conjunction**(AND)
    - p ∧ q<br/>
      |p|q|p ∧ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|F|
  - **Disjunction**(OR)
    - p ∨ q<br/>
      |p|q|p ∨ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Exclusive-Or**(XOR)
    - p ⊕ q<br/>
      |p|q|p ⊕ q|
      |:---:|:---:||:---:|
      |T|T|F|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Implication**(IMPLIES)
    - (Conditional Statement) 
    - p → q = ¬𝑝 ∨ q<br/>
      |p|q|p → q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|T|
      |F|F|T| 
    - **Converse**(역): q → p
    - **Inverse**(이): ¬𝑝 → ¬𝑞
    - **Contrapositive**(대우): ¬𝑞 → ¬𝑝
  - **Biconditional**(IFF)
    - p ↔ q<br/>
      |p|q|p ↔ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|T|
      
# Propositional Satisfiability
* **Satisfiable** Proposition: propositional variable에 하나라도 true를 넣었을때 결과로 True가 나오는 것
* **Unsatisfiable** Proposition: Not Satisfiable -> **Contradiction**
* **Valid** Proposition: 모든 결과가 True -> **Tautology**
  
