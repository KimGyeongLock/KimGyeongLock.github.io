---
layout: single
title: Ch 3. Arithmetic for computers - (3)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# Division

* Division = **‘adder’ (subtracter)** + **‘shifter’** registers
* Positive Integer에 대해서만 고려
* Algorithm
	If (partial remainder ≥ divisor) then
		quotient bit = 1;
		remainder = remainder - divisor;
	else
		quotient bit = 0;
	shift down next dividend bit
* Ex)<br/>
<img width="203" alt="스크린샷 2022-10-09 오전 1 03 14" src="https://user-images.githubusercontent.com/63464299/194717238-1780d77a-a5a4-46d8-b517-fc8570455b43.png">
    * 1000 (divisor)
    * 1001010 (dividend)
    * 1001 (quotient)
    * 10 (remainder)

## Division: Implementation
<img width="656" alt="스크린샷 2022-10-09 오전 1 05 54" src="https://user-images.githubusercontent.com/63464299/194717251-e69fa1b5-7db7-4ebe-a863-d9726fccc8df.png">

* Final Version을 활용
* Dividend
    * 64bits
    * Shift Right
    * Shift Left
    * register **Hi**
        * **Remainder** 저장
        * **mfhi** $t0
        * 32bits
    * register **Lo**
        * **Quotient** 저장
        * **mflo** $t1
        * 32bits

<img width="363" alt="스크린샷 2022-10-09 오전 1 12 51" src="https://user-images.githubusercontent.com/63464299/194717279-642bd59c-0b7a-4a40-9765-f0320cede170.png">


## Division of signed number
* Quotient
    * **Dividend와 Divisor의 sign**
        * 같으면 positive
        * 다르면 negative
* Remainder
    * **Dividend와 같은 sign**을 가짐
* Ex)
    * +7 / 2 = 3(Q) 1(R)
    * -7 / 2 = -3(Q) -1(R)
    * +7 / -2 = -3(Q) 1(R)
    * -7 / -2 = 3(Q) -1(R)
