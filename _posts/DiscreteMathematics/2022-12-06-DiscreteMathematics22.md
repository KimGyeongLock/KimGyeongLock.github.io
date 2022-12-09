---
layout: single
title: Boolean Algebra
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Boolean Expressions 
* 1 또는 0의 값에 대해 논리 동작을 다루는 대수
* **operators**
    * **\+ (Boolean sum)**
        * 1+0=1, 1+1=1
    * **∙ (Boolean product)**
        * 1∙1=1, 1∙0=0
    * **¯ (complement)**
        * ¯0 = 1, ¯1=0

-----------

# Boolean Functions
B= {0,1}<br/>
B^n = {(x1, x2, …, xn) | xi ∈ B for 1 ≤ i ≤ n}
* **Boolean variable** (x)
    * 0과 1만 가능한 변수 
* **Boolean function of degree n** (B^n → B)
    * f(B^n) = B
    * **degree n** = 변수의 갯수
        * 2^n개의 0과 1의 조합을 가짐 = 열의 갯수
    * **Boolean function of degree n 갯수 = 2^(2^n)**
* **Equivalent Functions**
    * 𝐹(𝑏1,𝑏2,...,𝑏𝑛) = 𝐺(𝑏1,𝑏2,...,𝑏𝑛)
    * F and G : equivalent
* **Complement of Function**<br/>
   <img width="282" alt="스크린샷 2022-12-06 오후 4 27 32" src="https://user-images.githubusercontent.com/63464299/205879657-5b6bd977-91e5-4938-ad7d-25c3684ffb49.png">

* **Sum / Product of Functions**
    * **Boolean sum**
        * (𝐹+𝐺)(𝑥1,𝑥2,…,𝑥n) = 𝐹(𝑥1,𝑥2,…,𝑥n) + 𝐺(𝑥1,𝑥2,…,𝑥n) 
    * **Boolean product**
        * (𝐹𝐺)(𝑥1,𝑥2,…,𝑥n) = 𝐹(𝑥1,𝑥2,…,𝑥n)𝐺(𝑥1,𝑥2,…,𝑥n) 
* **Identities** of Boolean Algebra
<img width="509" alt="스크린샷 2022-12-06 오후 4 51 44" src="https://user-images.githubusercontent.com/63464299/205879617-e635297d-f59a-473c-aa37-148929e50426.png">
> Each element of the pair is the dual of the other<br/>
> Law of the double complement, Unit property, Zero property 제외<br/>


-----------

# Representing Boolean Functions
* **Sum-of-Products Expansion**
    * 함수가 1의 값을 갖는 각 변수의 조합
    * F = x¯𝑦𝑧 = 1 (x=z=1, y=0) 
    * G = x𝑦¯𝑧 + ¯x𝑦¯𝑧 = 1 (x=y=1, z=0 or x=z=0, y=1) 
    *  = The sum of minterms that represents the function
    *  = **Disjunctive Normal Form**
* **Literal**
    * Boolean variable or its complement
* **Minterm**
    * 각 변수에 대해 하나의 literal을 가진 n literals의 곱
    * Boolean variables x1,x2,…,xn의  minterm<br/>= Boolean product y1y2⋯yn (yi=xi or yi=¯xi)
    * minterm y1y2⋯yn은 **value 1**을 가짐 ↔︎ 각 yi =1
    * xi=1 (yi=xi) , xi=0 (yi=¯xi)
      <img width="278" alt="스크린샷 2022-12-09 오후 10 46 04" src="https://user-images.githubusercontent.com/63464299/206716162-22ca1c2f-cef7-449c-9d55-973d8eed9b54.png">

* **Functional Completeness**
    * the set **{∙, + , ¯}**  = functionally complete
        * 모든 boolean function이 boolean operators를 사용해서 표현가능
    * **{∙, ¯}, {+ , ¯}** : functionally complete
    * **{\|}** (nand operator) : functionally complete
        * 1\|1 = 0, 1\|0 = 0\|1 = 0\|0 =1
        * **¯x** = x\|x, **xy** = (x\|y)\|(x\|y), **x+y** = (x\|x)\|(y\|y)
    * **{↓}** (nor operator) : functionally complete
        * 0↓0=1, 1↓0 = 0↓1 = 1↓1 = 0 
        * **¯x** = x↓x, **xy** = (x↓x)↓(y↓y), **x+y** = (x↓y)↓(x↓y)

-----------

# Logic Gates
