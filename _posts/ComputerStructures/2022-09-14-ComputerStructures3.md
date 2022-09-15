---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(2)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Introduction to Instruction Set Architecture
# - The number of operands

## Number of Operands
* **Three Operands** (MIPS Normally)
    * ADD A, B, C
        * Destination: A
        * Sources: B and C
        * (A ← B + C) or (C ← A + B)
* **Two Operands**
    * ADD A, B
        * Destination: A
        * Sources: A and B
        * (A ← A + B)
* **One Operand**
    * ADD A
        * Destination: **AC(Accumulator)**
        * Sources: A and AC
        * (AC ← AC + A)
    * LD(Load) A
        * Destination: AC
        * Source: A
        * (AC ← A)
* **Zero Operand**
    * PUSH A (TOS(Top Of Stack) ← A)
    * PUSH B (TOS ← B)
    * **ADD** (TOS ← A+B)
        * do not need an address field -> Zero Operand
    * POP C (C ← TOS)


## The number of address field
Ex) op code: 5 bits, each address fields: 12 bits<br/>
→ 3 addr. inst. mach. : 5 + 3x12 = 41bits<br/>
→ 2 addr. inst. mach. : 5 + 2x12 = 29bits<br/>
→ 1 addr. inst. mach. : 5 + 1x12 = 17bits<br/>

=> address↑ bus(Processor와 Memory간의 이동) wider, instructions의 개수↓<br/>
컴퓨터는 기본적으로 32bits (MIPS) → 버스는 한번에 32bits까지 옮길 수 있다.<br/>
→ 32bits보다 큰 경우 bits를 쪼개거나 더 큰 버스를 이용 -> 더 큰 Cost발생<br/>


## Exercise
Z = (A+B)/C<br/>
<u>instruction이 줄어들면 연산량이 줄어든다</u>

* Three Operands
    * ADD Z,A,B (Z←A+B)<br/>
      DIV Z,Z,C (Z←Z/C)

    * ADD A,A,B (A←A+B)<br/>
      DIV Z,A,C (Z←A/C)<br/>
      => A 원본의 손상

* Two Operands<br/>
  ‘MOV(move)’, ‘CLR(clear)’ extra instruction<br/>
   T(temp extra space)<br/>
    * MOV T,A (T←A)<br/>
      ADD T,B (T←T+B)<br/>
      DIV T,C (T←T(A+B)/C)<br/>
      MOV Z,T (Z←T)

    * MOV Z,A (Z←A)<br/>
      ADD Z,B (Z←Z+B)<br/>
      DIV Z,C (Z ← Z/C)

    * CLR Z (Z=0)<br/>
      ADD Z,A (Z←Z+A)<br/>
      ADD Z,B (Z←Z+B)<br/>
      DIV Z,C (Z←Z/C)

* One operand<br/>
  ‘MOV’
    * MOV A (AC←A)<br/>
      ADD B (AC←AC(A)+B)<br/>
      DIV C (AC←AC(A+B)/C)<br/>
      MOV Z (Z←AC)<br/>
      => definition problem

    * LOAD A (AC←A)<br/>
      ADD B (AC←AC+B)<br/>
      DIV C (AC←AC/C)<br/>
      STORE Z (Z←AC)

* Zero operand
    * PUSH A (TOS←A)<br/>
      PUSH B (TOS←B)<br/>
      ADD (TOS←A+B)<br/>
      PUSH C (TOS←C)<br/>
      DIV (TOS←(A+B)/C)<br/>
      POP Z (Z←TOS)
