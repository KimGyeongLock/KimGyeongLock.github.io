---
layout: single
title: Ch 3. Arithmetic for computers
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Addition and Subtraction

## Integer Addition
* two’s complement 가정
* Overflow가 발생하는 경우
    * magnitude가 너무 커져 숫자를 표현할 수 없을 때
    * **Positive Operand + Positive Operand** = Result(**Sign = 1**)
        * sign = 1(Negative)
    * **Negative Operand + Negative Operand** = Result(**Sign = 0**)
        * sign = 0(Positive or 0)

## Integer Subtraction
* 7 - 6 = 7 + (-6)
* Overflow가 발생하는 경우
    * **Positive Operand - Negative Operand** = Result(**Sign = 0**)
        * sign = 0(Positive or 0)
    * **Negative Operand - Positive Operand** = Result(**Sign = 1**)
        * sign = 1(Negative)

## Dealing with Overflow
1. Some languages (C)
    * **overflow 무시**
    * MIPS
        * **addu, addiu, subu** instructions
        * **u(unsigned)**
2. Other languages (Ada, Fortran..)
    * **프로그래머한테 에러 발생을 알림**
    * invoke exception handler
