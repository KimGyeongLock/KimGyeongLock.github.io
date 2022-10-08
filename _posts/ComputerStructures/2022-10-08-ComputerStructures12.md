---
layout: single
title: Ch 3. Arithmetic for computers - (2)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# Multiplication

* Multiplying = ‘add’ + ‘shift’ operation
    * with binary numbers
* Positive integer에 대해서만 고려
* Ex)<br/>
    <img width="197" alt="스크린샷 2022-10-08 오후 10 33 23" src="https://user-images.githubusercontent.com/63464299/194712821-888b2762-5584-40f6-9585-de9ce9eebff1.png">
    * 0010 (multiplicand)
    * 1001 (multiplier)
    * 0010010 (product)
    

## Multiplication: Implementation
* Version 1<br/>
  <img width="765" alt="스크린샷 2022-10-08 오후 11 29 49" src="https://user-images.githubusercontent.com/63464299/194712836-42771eb6-0aa5-43ff-86b4-1a207d026c47.png">
    * Multiplicand: **Shift Left**
    * Product: doesn’t move
    * Multiplicand: 64bits
    * Multiplier: 32bits
    * Product: 64bits
    * 64-bit ALU
* Version 2<br/>
    <img width="749" alt="스크린샷 2022-10-08 오후 11 30 07" src="https://user-images.githubusercontent.com/63464299/194712854-ca353972-c8bc-43a2-b172-fd25767f8b37.png">
    * Multiplicand: doesn’t move
    * Product: **Shift Right**
    * Multiplicand: 32bits
    * Multiplier: 32bits
    * Product: 64bits
    * 32-bit ALU
* Version 1 → Version2: **Save Spaces & Hardware reducing**
* **Final Version**<br/>
    <img width="722" alt="스크린샷 2022-10-08 오후 11 30 31" src="https://user-images.githubusercontent.com/63464299/194712859-75dac2c7-f153-4392-8303-e1fe3c4dfba3.png">
    * Multiplier -> Product register
    
    <img width="462" alt="스크린샷 2022-10-08 오후 11 31 49" src="https://user-images.githubusercontent.com/63464299/194712869-f0e4664d-d6ba-4763-ba31-340b6323fbeb.png">


## Multiplication of negative numbers
1. Negate negative number(s)
    * -3 => 3
2. unsigned multiplication 수행
    * 3 * 4 = 12
3. negate the result
    * 12 => -12

* Another way: Booth algorithm
