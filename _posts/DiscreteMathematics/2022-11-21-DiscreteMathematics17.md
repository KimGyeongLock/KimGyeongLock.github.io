---
layout: single
title: Discrete Probability3
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Random Variables
* **Random Variable**
    * **function**
        * preimage: sample space of an experiment
        * image: the set of real numbers
    * 각 가능한 결과에 실수가 할당
    
--------

# Expected Value
* **Expected Value (기댓값)**<br/>
<img width="136" alt="스크린샷 2022-11-21 오전 1 19 48" src="https://user-images.githubusercontent.com/63464299/202916645-f11e6780-8aca-453a-b326-7473e7bbc826.png">
    * X(s): 랜덤변수
    * S: sample space
* Theorem 1
    * p(X = r): 랜덤변수 X = r일 때 확률(probability)<br/>
<img width="157" alt="스크린샷 2022-11-21 오전 1 24 20" src="https://user-images.githubusercontent.com/63464299/202916657-8745a8bf-c115-4a21-8c6f-a87c68a14ecb.png">
* Theorem 2
    * 성공의 기댓값 = **np**
        * n: 상호 독립적인 베르누이 시행이 수행될 때,
        * p: 각 시행의 성공 확률
* Theorem 3
    * Linearity of Expectations
        * **E(X1+X2+⋯ +Xn)** = **E(X1) + E(X2) + ⋯ + E(Xn)**
        * **E(aX + b) = aE(X) + b**
* Theorem 4
    * **Geometric Distribution(기하분포)**
        * 동일한 베르누이 분포를 따르는 시행의 독립적인 반복에서 처음으로 성공하기까지의 시도횟수를 확률변수로 가지는 분포
    * p(X = k) = (1-p)^(k-1)p
    * **E(X) = 1/p**
* Theorem 5
    * **Independent Random Variables**
        * 𝑝(𝑋 = 𝑟1 and 𝑌 = 𝑟2) = 𝑝(𝑋 = 𝑟1)∙𝑝(𝑌 = 𝑟2) -> 랜덤변수 X와 Y는 독립
    * 랜덤변수 X와 Y는 독립 -> **E(XY) = E(X)E(Y)**

# Variance of Random Variables
* **편차(Deviation)**
    * X(s) - E(X)
* **분산(Variance)**
    * 편차 제곱의 가중 평균<br/>
  <img width="193" alt="스크린샷 2022-11-21 오전 2 12 50" src="https://user-images.githubusercontent.com/63464299/202916739-18e6d6fd-89a8-41c7-b8aa-8ec42b869c55.png">
    * 표준 편차 𝜎(𝑋) = √𝑉(𝑋)  
* Theorem
    * **V(X) = E(X^2) - (E(X))^2**
* Corollary
    * E(X) = 𝜇, then 𝑉(𝑋) = 𝐸((𝑋 − 𝜇)^2) 
* Bienaymé‘s Formula
    * V(𝑋1+𝑋2+⋯+𝑋n) =V(𝑋1) +V(𝑋2) +⋯+ V(𝑋n) 
    * **V(Xi) = pq**
    * **V(X) = npq**
* Chebyschev’s Inequality(체비쇼프의 부등식)
    * 𝑝(\|𝑋(𝑠) − 𝐸(𝑋)\|≥𝑟) ≤ V(𝑋)/𝑟^2 

