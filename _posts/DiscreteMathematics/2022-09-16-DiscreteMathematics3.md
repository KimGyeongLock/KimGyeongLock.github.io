---
layout: single
title: Proofs (Rules of Inference)
toc: true
toc_sticky: true
categories: Discrete
published: true
---

Prove: the Socrates Example is valid (using **the rules of inference**)
=====================================

# Arguments in propositional logic
* a sequence of propositions
    * premises (all proposition except final)
    * conclusion(∴) (last proposition)

The argument is valid **if the premises imply the conclusion**<br/>
Argument form with premises p1, p2, … pn and conclusion q is valid when (p1 ∧ p2 ∧  … ∧ pn) -> q is a tautology

------------

# Rules of Inference for Propositional Logic

## Modus Ponens(MP, 긍정논법)
= implication elimination(함의소거)<br/>
= affirming the antecedent(전건긍정)<br/>
* 가언 명제(만약if,”→”)와 그 전제로부터 그 **결론**을 유도해내는 추론 규칙
* (“만약 P이면, Q이다”와 “P이다”)에서 “Q이다”를 추론
* (𝑝∧(𝑝→𝑞))→𝑞 


## Modus Tollens(MT, 부정논법)
= denying the consequent(후건부정)<br/>
* 가언 명제와 그 결론의 부정으로부터 그 **전제의 부정**을 유도하는 추론 규칙
* (“만약 P라면, Q이다. 그런데 Q가 아니다.) 따라서 P가 아니다를 추론
* (¬𝑞∧(𝑝→𝑞))→¬𝑝 


## Hypothetical Syllogism(가언적 삼단 논법)
* 두 개의 가언 명제로부터 추이성을 통해 새로운 **가언 명제**를 유도하는 삼단 논법
* “만약 P라면, Q이다. 만약 Q라면, R이다. 따라서, 만약 P라면, R이다.”
* ((𝑝→𝑞)∧(𝑞→𝑟)) →(𝑝→𝑟 )


## Disjunctive Syllogism(선언적 삼단 논법)
* 선언 명제(또는or)와 이를 이루는 두 명제 가운데 하나에 대한 부정으로부터 다른 한 명제를 유도하는 삼단 논법
* “P가 참이거나 Q가 참이다. 그런데 P는 참이 아니다. 따라서 Q가 참이다.”
* (¬𝑝∧(𝑝∨𝑞)) →𝑞 

## Addition(가산 논법)
* 𝑝→(𝑝∨𝑞)
* Or Operator 에서 Add 

## Simplification(단순화 논법)
* (𝑝∧𝑞)→𝑝 
* And Operator 에서 Simplification

## Conjunction(논리곱 논법)
* ((𝑝)∧(𝑞))→(𝑝∧𝑞) 

## Resolution(분해)
* ((¬𝑝∨𝑟) ∧ (𝑝∨𝑞)) → (𝑞∨𝑟) 

-------------

# Valid Arguments

“It is not sunny this afternoon and it is colder than yesterday.” (¬p ∧ q)<br/>
“We will go swimming only if it is sunny.” => “If we go swimming then it is sunny.” (r → p)<br/>
“If we do not go swimming, then we will take a canoe trip.” (¬r → s)<br/>
“If we take a canoe trip, then we will be home by sunset.”  (s → t)<br/>
<br/>
p: It is sunny this afternoon<br/>
q: it is colder than yesterday<br/>
r: we will go swimming<br/>
s: we will take a canoe trip<br/>
t: we will be home by sunset<br/>

* Steps
1. premise
2. simplification ¬p ∧ q => (¬p)
3. premise r → p
4. Modus tollens (¬r)
5. premise ¬r → s
6. Modus Ponens (s)
7. premise s → t 
8. Modus Ponens (t)



# Handling Quantified Statements

* **Universal Instantiation** (**UI**, 전칭 예시화)
    * 모든 x 에 대하여 P(x) 가 참이면, P(c) 는 참이다.
* **Universal Generalization** (**UG**, 전칭 일반화)
    * 임의의 c 에 대하여 P(c) 가 참이면, 모든 x 에 대해 P(x) 는 참이다.
* **Existential Instantiation** (**EI**, 존재 예시화)
    
* **Existential Generalization** (**EG**, 존재 일반화)

## Exercise

* Conclusion
  - John Smith has two legs
 
* Premises
  - Every man has two legs -> ∀x(M(x) → L(x)) 
  - John Smith is a man  -> M(John)

* Solution 
  * M(x): x is a man
  * L(x): x has two legs

  * Premise : ∀x(M(x) -> L(x)) 
  * UI From : M(John) -> L(John)
  * Premise: M(John)
  * Modus Ponens: L(John)


* Conclusion 
  - Someone who passed the first exam has not read the book

* Premises
  - A student in this class has not read the book -> ∃x((C(x) ∧ ¬B(x))
  - Everyone in this class passed the first exam -> ∀x(C(x) → P(x))

* Solution
  * C(x): x is in this class
  * B(x): x has read the book 
  * P(x): x passed the first exam

  * Premise : ∃x((C(x) ∧ ¬B(x))
  * EI : C(Someone) ∧ ¬B(Someone)
  * Simplification: C(Someone)
  * Premise : ∀x(C(x) → P(x))
  * UI : C(Someone) -> P(Someone)
  * MP: P(Someone)
  * Simplification : ¬B(Someone)
  * Conjunction : P(Someone) ∧ ¬B(Someone)
  * EG : ∃x((P(x) ∧ ¬B(x))


### Socartes Example

* Conclusion
  - Socrates is mortal

* Premises
  - All men are mortal -> ∀x(Man(x) → Mortal(x))
  - Socrates is a man -> Man(Socrates)

* Solution
  * Man(x): x is a man
  * Mortal(x): x is mortal

  * Premise : ∀x(Man(x) → Mortal(x))
  * UI : Man(Socrates) -> Mortal(Socrates)
  * Premise : Man(Socrates)
  * MP : Mortal(Socrates)


* **Universal Modus Ponens**
    * UI + MP
    * be used in the Socrates example.

