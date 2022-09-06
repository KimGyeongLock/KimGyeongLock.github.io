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
    - <span style="color: red">**¬**</span>p
    - |p|¬p|
      |:---:|:---:|
      |T|F|
      |F|T|
  
  - **Conjunction**(AND)
    - p <span style="color: red">**∧**</span> q
    - |p|q|p ∧ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|F|
  - **Disjunction**(OR)
    - p <span style="color: red">**∨**</span> q
    - |p|q|p ∨ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Exclusive-Or**(XOR)
    - p <span style="color: red">**⊕**</span> q
    - |p|q|p ⊕ q|
      |:---:|:---:||:---:|
      |T|T|F|
      |T|F|T|
      |F|T|T|
      |F|F|F|
  - **Implication**(IMPLIES)
    - (Conditional Statement) 
    - p <span style="color: red">**→**</span> q
    - |p|q|p → q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|T|
      |F|F|T| 
    - p(약속, hypothesis), q(약속을 지키는 거, conclusion)
    - q는 p의 필요조건 
    - p는 q의 충분조건
    - **Converse**(역): q → p
    - **Inverse**(이): ¬p → ¬q
    - **Contrapositive**(대우): ¬q → ¬p
  - **Biconditional**(IFF)
    - p <span style="color: red">**↔**</span> q
    - |p|q|p ↔ q|
      |:---:|:---:||:---:|
      |T|T|T|
      |T|F|F|
      |F|T|F|
      |F|F|T|
    
    - 필요 충분 조건
    
# Equivalent Propositions
* If two propositions always the same truth value -> **Equivalent**
* <span style="color: red">**≡**</span>
* p → q ≡ ¬q → ¬p(contrapositive)
* <span style="color: red">**p → q ≡ ¬p ∨ q**</span> (truth table)

# Precedence of Logical Operators
1. **¬**(Negation)
2. **∧**(Conjunction)
3. **∨**(Disjunction)
4. **→**(Implication)
5. **↔**(Biconditional)

# Propositional Equivalences
* **Tautology**(동어반복)
  * always **True**
  * Ex) p ∨ ¬p
* **Contradiction**(모순)
  * always **False**
  * Ex) p ∧ ¬p
* **Contingency**(우연)
  * not tautology ∧ not contradiction
* ![propositional+logic](https://user-images.githubusercontent.com/63464299/183473997-f5504f2a-f873-4377-bd89-c77699ad6086.jpg)
* **De Morgan's law**: ¬(p ∧ q) ≡ ¬p ∨ ¬q, ¬(p ∨ q) ≡ ¬p ∧ ¬q
* Negation Laws: p ∨ ¬q ≡ T, p ∧ ¬p ≡ F
* Absorption Laws: p ∨ (p ∧ q) ≡ p, p ∧ (p ∨ q) ≡ p
 
 
# Propositional Satisfiability
* **Satisfiable** Proposition: **적어도 하나**의 case가 True
* **Unsatisfiable** Proposition: All case is False -> **Contradiction**(모순)
* **Valid** Proposition: 모든 결과가 True -> **Tautology**
  
# Notation
∨^𝑛𝑗=1
