---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(5)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 2. Binary Number Basic

## Unsigned Binary Integers
<img width="251" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/192540428-2b8f7e93-a766-4081-99e6-2bc849ee9fab.png">
* Range: 0 to +2^n - 1
* Using 32 bits
    * 0 to +4,294,967,295
* Ex)
    * 0000 0000 0000 0000 0000 0000 0000 1011<br/>
      = 0 + ••• + 1×2^3 + 0×2^2 + 1×2^1 + 1×2^0<br/>
      = 0 + ••• + 8 + 0 + 2 + 1 = 11

## Negative Number Representations
|Sign Magnitude|One’s Complement|Two’s Complement|
|:—:|:—:|:—:|
|000 = +0|000 = +0|000 = +0|
|001 = +1|001 = +1|001 = +1|
|010 = +2|010 = +2|010 = +2|
|011 = +3|011 = +3|011 = +3|
|100 = -0|100 = -3|100 = -4|
|101 = -1|101 = -2|101 = -3|
|110 = -1|110 = -1|110 = -2|
|111 = -2|111 = -0|111 = -1|

* Two’s Complement
    * 0을 나타내는 숫자가 하나
    * 더 많은 숫자를 표현
    * ease of operations
* Exercise
    * -11: 0 000 1011
    * signed magnitude
        * 1 000 1011
    * one’s complement
        * 1 111 0100
    * two’s complement
        * 1 111 0101

## 2s-Complement Signed Integers
<img width="261" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/192540501-ead88c13-b0bc-4494-b881-8c50a8381744.png">
* Range: -2^n-1 to +2^n-1 - 1
* Using 32 bits
    * -2,147,483,648 to +2,147,483,647
* Ex)
    * 1111 1111 1111 1111 1111 1111 1111 1100<br/>
      = -1×2^31 + 1×2^30 + ••• + 1×2^2 + 0×2^1 + 0×2^0
      = -2,147,483,648 + 2,147,483,644 = -4


## Signed Negation
* **Complement and add 1**
* Ex) Negate +2
    * +2 = 0000 0000 ••• 0010
    * -2 = 1111 1111 ••• 1101 + 1 = 1111 1111 ••• 1110
