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
        * Destination: AC(Accumulator)
        * Sources: A and AC
        * (AC ← AC + A)
    * LD(Load) A
        * Destination: AC
        * Source: A
        * (AC ← A)
* **Zero Operand**
    * PUSH A (TOS(Top Of Stack) ← A)
    * PUSH B (TOS ← B)
    * ADD (TOS ← A+B)
        * do not need an address field -> Zero Operand
    * POP C (C ← TOS)


## The number of address field
Ex) op code: 5 bits, each address fields: 12 bits<br/>
→ 3 addr. inst. mach. : 5 + 3x12 = 41bits<br/>
→ 2 addr. inst. mach. : 5 + 2x12 = 29bits<br/>
→ 1 addr. inst. mach. : 5 + 1x12 = 17bits<br/>

=> address가 많아질수록 bus(Processor와 Memory간의 이동)가 넓어지고 instructions의 개수가 작아진다.<br/>
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

    * LOAD A<br/>
      ADD B<br/>
      DIV C<br/>
      STORE Z

* Zero operand
    * PUSH A (TOS←A)<br/>
      PUSH B (TOS←B)<br/>
      ADD (TOS←A+B)<br/>
      PUSH C (TOS←C)<br/>
      DIV (TOS←(A+B)/C)<br/>
      POP Z (Z←TOS)


# - Addressing modes
* operand가 메모리나 레지스터에 있는 장소를 지정하는 다양한 방법
* Advantages
    * 프로그래밍 다양성
        * pointers to memory
        * counters for loop control
        * indexing of data
    * addressing field의 비트 수 감소
* **Effective Address(E.A.)**
    * Actual address of the location containing the referenced operand
    * ex) In ARM  LDR(Load cpu의 register) r1, [r2, #20]
        * <img width="592" alt="스크린샷 2022-09-14 오후 12 48 18" src="https://user-images.githubusercontent.com/63464299/190156153-f3ef6bc6-da03-4e74-968a-9c510f079f4e.png">
        * Effective Address: 120
        * #: 값 자체, 날 것 그대로의 데이터
    * ex) In MIPS  lw(load word) $t1, 1000($s1)
        * <img width="601" alt="스크린샷 2022-09-14 오후 8 16 28" src="https://user-images.githubusercontent.com/63464299/190156160-1e9df0c9-6359-408a-8a17-de849033c2b0.png">
        * Effective Address: 1100
        * $: register


1. **Implied** addressing mode 
	* No explicit address
	* 명령어 실행에 필요한 operand를 지정하지 않아도 묵시적으로 수행하는 방식
2. **Immediate** addressing mode(즉시 주소 지정 방식)
	* Operand field contains the actual operand value 
	* operand에 연산에 필요한 숫자 데이터를 직접 넣어주는 방식
	* 명령어 자신이 데이터를 직접 포함하고 있어 명령어의 실행이 바로 이루어지는 방법
	* ex) In ARM ADD r3, r3, #4
	  * r3←r3+4
	* ex) In MIPS  addi $s1, $s2, 4
		* s1←s2+4
		* addi(immediate address) address랑 다름
