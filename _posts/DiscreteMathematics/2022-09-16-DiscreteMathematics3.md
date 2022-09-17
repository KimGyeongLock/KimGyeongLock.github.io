---
layout: single
title: Proofs (Rules of Inference)
toc: true
toc_sticky: true
categories: Discrete
published: true
---

Prove: the Socrates Example is valid (using **the rules of inference**)


# Arguments in propositional logic
* a sequence of propositions
    * **premises** (all proposition except final)
    * **conclusion(∴)** (last proposition)

The argument is valid **if the premises imply the conclusion**<br/>
Argument form with premises p1, p2, … pn and conclusion q is **valid** 
<br/>when (p1 ∧ p2 ∧  … ∧ pn) -> q is a **tautology**

------------

# Rules of Inference for Propositional Logic

## Modus Ponens(MP, 긍정논법)
= implication elimination(함의소거)<br/>
= affirming the antecedent(전건긍정)<br/>
* 가언 명제(만약if,”→”)와 그 전제로부터 그 **결론**을 유도해내는 추론 규칙
* (“만약 P이면, Q이다”와 “P이다”)에서 “Q이다”를 추론
* (𝑝∧(𝑝→𝑞))→𝑞<br/>
<img width="94" alt="스크린샷 2022-09-17 오후 2 15 20" src="https://user-images.githubusercontent.com/63464299/190841710-ad350068-d600-45a6-bc80-a73b00ea6f36.png">


## Modus Tollens(MT, 부정논법)
= denying the consequent(후건부정)<br/>
* 가언 명제와 그 결론의 부정으로부터 그 **전제의 부정**을 유도하는 추론 규칙
* (“만약 P라면, Q이다. 그런데 Q가 아니다.) 따라서 P가 아니다를 추론
* (¬𝑞∧(𝑝→𝑞))→¬𝑝<br/>
<img width="126" alt="스크린샷 2022-09-17 오후 2 15 47" src="https://user-images.githubusercontent.com/63464299/190841715-29aafd84-b88c-4105-be1c-1bf0d8e8ca91.png">
* Contrapositive(대우)<br/>
   (¬q∧(¬q→¬p)) → ¬p


## Hypothetical Syllogism(가언적 삼단 논법)
* 두 개의 가언 명제로부터 추이성을 통해 새로운 **가언 명제**를 유도하는 삼단 논법
* “만약 P라면, Q이다. 만약 Q라면, R이다. 따라서, 만약 P라면, R이다.”
* ((𝑝→𝑞)∧(𝑞→𝑟)) →(𝑝→𝑟 )<br/>
<img width="139" alt="스크린샷 2022-09-17 오후 2 16 06" src="https://user-images.githubusercontent.com/63464299/190841717-34fbb122-c599-4eff-b315-150234714ea7.png">


## Disjunctive Syllogism(선언적 삼단 논법)
* 선언 명제(또는or)와 이를 이루는 두 명제 가운데 하나에 대한 부정으로부터 다른 한 명제를 유도하는 삼단 논법
* “P가 참이거나 Q가 참이다. 그런데 P는 참이 아니다. 따라서 Q가 참이다.”
* (¬𝑝∧(𝑝∨𝑞)) →𝑞<br/>
<img width="74" alt="스크린샷 2022-09-17 오후 2 16 22" src="https://user-images.githubusercontent.com/63464299/190841720-ac6756a2-3340-4b0f-a856-30a12ab0da6a.png">


## Addition(가산 논법)
* 𝑝→(𝑝∨𝑞)<br/>
<img width="133" alt="스크린샷 2022-09-17 오후 2 16 39" src="https://user-images.githubusercontent.com/63464299/190841734-9a141916-f297-418e-a267-5482029eb497.png">

* Or Operator 에서 Add 

## Simplification(단순화 논법)
* (𝑝∧𝑞)→𝑝<br/>
<img width="94" alt="스크린샷 2022-09-17 오후 2 16 50" src="https://user-images.githubusercontent.com/63464299/190841740-fcc0f728-3a85-4198-9914-abe66b759d13.png">

* And Operator 에서 Simplification

## Conjunction(논리곱 논법)
* ((𝑝)∧(𝑞))→(𝑝∧𝑞)<br/>
<img width="91" alt="스크린샷 2022-09-17 오후 2 17 02" src="https://user-images.githubusercontent.com/63464299/190841749-164c016f-dd27-49ba-bd99-9bc41a45ad00.png">


## Resolution(분해)
* ((¬𝑝∨𝑟) ∧ (𝑝∨𝑞)) → (𝑞∨𝑟)<br/>
<img width="127" alt="스크린샷 2022-09-17 오후 2 17 14" src="https://user-images.githubusercontent.com/63464299/190841754-d6671623-ad08-4797-a12f-630f2ed2d6be.png">


-------------

# Valid Arguments

“It is not sunny this afternoon and it is colder than yesterday.” (¬p ∧ q)<br/>
“If we go swimming then it is sunny.” (r → p)<br/>
“If we do not go swimming, then we will take a canoe trip.” (¬r → s)<br/>
“If we take a canoe trip, then we will be home by sunset.”  (s → t)<br/>
**Hypotheses**: ¬p ∧ q, r → p, ¬r → s, s → t<br/>
<br/>
p: It is sunny this afternoon<br/>
q: it is colder than yesterday<br/>
r: we will go swimming<br/>
s: we will take a canoe trip<br/>
t: we will be home by sunset<br/>

* Solution<br/>

   |Step|Reason|
   |:---:|:---:|
   |1. ¬p∧q|Premise|
   |2. ¬p|Simplification using (1)|
   |3. r→p|Premise|
   |4. ¬r|Modus tollens using (2) and (3)|
   |5. ¬r→s|Premise|
   |6. s|Modus ponens using (4) and (5)|
   |7. s→t|Premise|
   |8. t(**Conclusion**)|Modus ponens using (6) and (7)|


# Handling Quantified Statements

* **Universal Instantiation** (**UI**, 전칭 예시화)
    * <img width="102" alt="스크린샷 2022-09-17 오후 3 58 51" src="https://user-images.githubusercontent.com/63464299/190844827-8ae3a7fd-37bc-4c79-a30d-90eb83609a0a.png">
    * 모든 x 에 대하여 P(x) 가 참이면, P(c) 는 참이다.
* **Universal Generalization** (**UG**, 전칭 일반화)
    * <img width="275" alt="스크린샷 2022-09-17 오후 3 56 11" src="https://user-images.githubusercontent.com/63464299/190844839-3146ca9d-f481-4781-89e5-305bb26798cc.png">
    * 임의의 c 에 대하여 P(c) 가 참이면, 모든 x 에 대해 P(x) 는 참이다.
* **Existential Instantiation** (**EI**, 존재 예시화)
    * <img width="316" alt="스크린샷 2022-09-17 오후 3 56 24" src="https://user-images.githubusercontent.com/63464299/190844852-5a4ea0f5-d096-4f50-8b5e-0455f1855315.png">
    * "There is someone who ~"
* **Existential Generalization** (**EG**, 존재 일반화)
    * <img width="297" alt="스크린샷 2022-09-17 오후 3 56 37" src="https://user-images.githubusercontent.com/63464299/190844931-ea13c038-4997-4ae5-973a-202355375e65.png">

## Exercise

### #1.
* Conclusion
  - John Smith has two legs
 
* Premises
  - Every man has two legs -> ∀x(M(x) → L(x)) 
  - John Smith is a man  -> M(John)

* Solution 
  * M(x): x is a man
  * L(x): x has two legs
   <br/>
  1. ∀x(M(x) -> L(x)): Premise 
  2. M(John) -> L(John): UI
  3. M(John): Premise
  4. L(John): Modus Ponens

### #2.
* Conclusion 
  - Someone who passed the first exam has not read the book

* Premises
  - A student in this class has not read the book -> ∃x((C(x) ∧ ¬B(x))
  - Everyone in this class passed the first exam -> ∀x(C(x) → P(x))

* Solution
  * C(x): x is in this class
  * B(x): x has read the book 
  * P(x): x passed the first exam

  1. ∃x((C(x) ∧ ¬B(x)): Premise
  2. C(Someone) ∧ ¬B(Someone): EI
  3. C(Someone): Simplification 
  4. ∀x(C(x) → P(x)): Premise 
  5. C(Someone) -> P(Someone): UI
  6. P(Someone): MP
  7. ¬B(Someone): Simplification (2)
  8. P(Someone) ∧ ¬B(Someone): Conjunction
  9. ∃x((P(x) ∧ ¬B(x)): EG


### #3. Socartes Example

* Conclusion
  - Socrates is mortal

* Premises
  - All men are mortal -> ∀x(Man(x) → Mortal(x))
  - Socrates is a man -> Man(Socrates)

* Solution
  * Man(x): x is a man
  * Mortal(x): x is mortal

  1. ∀x(Man(x) → Mortal(x)): Premise
  2. Man(Socrates) -> Mortal(Socrates): UI
  3. Man(Socrates): Premise
  4. Mortal(Socrates): MP


* **Universal Modus Ponens**
    * UI + MP
    * be used in the Socrates example.

