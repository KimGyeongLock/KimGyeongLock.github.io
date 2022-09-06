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

------------

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
 
------------ 
    
# Equivalent Propositions
* If two propositions always the same truth value -> **Equivalent**
* <span style="color: red">**≡**</span>
* p → q ≡ ¬q → ¬p(contrapositive)
* <span style="color: red">**p → q ≡ ¬p ∨ q**</span> (truth table)

------------

# Precedence of Logical Operators
1. ¬ (Negation)
2. ∧ (Conjunction)
3. ∨ (Disjunction)
4. → (Implication)
5. ↔ (Biconditional)

------------

# Propositional Equivalences
* **Tautology**(동어반복)
  * always **True**
  * Ex) p ∨ ¬p
* **Contradiction**(모순)
  * always **False**
  * Ex) p ∧ ¬p
* **Contingency**(우연)
  * not tautology ∧ not contradiction
* <br/>![propositional+logic](https://user-images.githubusercontent.com/63464299/183473997-f5504f2a-f873-4377-bd89-c77699ad6086.jpg)
* **De Morgan's law**: ¬(p ∧ q) ≡ ¬p ∨ ¬q, ¬(p ∨ q) ≡ ¬p ∧ ¬q
* Negation Laws: p ∨ ¬q ≡ T, p ∧ ¬p ≡ F
* Absorption Laws: p ∨ (p ∧ q) ≡ p, p ∧ (p ∨ q) ≡ p
 
------------ 
 
# Propositional Satisfiability
* **Satisfiable** Proposition: **적어도 하나**의 case가 True
* **Unsatisfiable** Proposition: All case is False -> **Contradiction**(모순)
* **Valid** Proposition: 모든 결과가 True -> **Tautology**
  
------------  
  
# Notation
<img width="87" alt="스크린샷 2022-09-06 오후 2 25 58" src="https://user-images.githubusercontent.com/63464299/188553792-eaf4034b-9e63-4abb-86b7-493a6feaf3ab.png">
> p1 ∨ p2 ∨ ... pn

<img width="89" alt="스크린샷 2022-09-06 오후 2 26 37" src="https://user-images.githubusercontent.com/63464299/188553991-05f62f35-babb-4e98-bb68-d5d78858c4d6.png">
> p1 ∧ p2 ∧ ... pn

------------

# N-Queen Problem

* Place N Queens on a NxN grid
* Don't place two Queens on the same vertical, horizontal or diagonal line
* Proposition p𝑖,𝑗: i행, j열에 있는 퀸
  * Queen이 있으면 True, 없으면 False

* Algorithm<br/>
 𝑄 = 𝑄1 ∧ 𝑄2 ∧ 𝑄3 ∧ 𝑄4 ∧ 𝑄5
    1. 모든 행은 최소 한개의 퀸을 포함<br/>
        <img width="170" alt="스크린샷 2022-09-06 오후 4 46 58" src="https://user-images.githubusercontent.com/63464299/188577388-4e89747d-c218-40f1-a99c-76de21640bf6.png">
    2. 각 행에 최대 한개의 퀸만 존재<br/>
        <img width="287" alt="스크린샷 2022-09-06 오후 5 12 08" src="https://user-images.githubusercontent.com/63464299/188582507-4456fd51-9685-47ff-a354-a5e116a77ac3.png">
    3. 각 열에 최대 하나의 퀸만 존재<br/>
        <img width="304" alt="스크린샷 2022-09-06 오후 4 47 46" src="https://user-images.githubusercontent.com/63464299/188582400-69e2e826-89b6-419d-96b2-f58d94ec7eb5.png">
    4. top-right 방향 대각선에 2개 이상의 퀸이 존재X<br/>
        <img width="384" alt="스크린샷 2022-09-06 오후 4 48 00" src="https://user-images.githubusercontent.com/63464299/188577492-6b36795d-57ec-4309-8012-721a86e9a482.png">
    5. bottom- right 방향 대각선에 2개 이상의 퀸이 존재X<br/>
        <img width="386" alt="스크린샷 2022-09-06 오후 4 48 15" src="https://user-images.githubusercontent.com/63464299/188577534-66ee3ae8-f486-439b-965e-b7fb13fb0dd6.png">
