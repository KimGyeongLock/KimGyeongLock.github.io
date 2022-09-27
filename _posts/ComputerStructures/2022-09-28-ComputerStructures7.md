---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(6)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 3. MIPS Design Principles

## MIPS ISA Key Idea
* Goals of instruction set design for MIPS
    * **Maximize performance**
    * **Minimize cost**
    * **Reduce design time** (of compiler and hardware)
    * RISC: By the **simplicity** of Hardware


## MIPS Register Model
* **32 x 32bits General Purpose Registers**(범용 레지스터) (Integer)
    * R0 always = 0
    * R0~R31 : 32Bits register
* **32 x 32 bits Floating Point Registers**
    * 16 x 64 bits (double precision)
    * even reg: less-significant word
    * odd reg: more-significant word
* **HI** (32bits), **LO**(32bits)
    * 곱하기(총 64bits) 나누기(Q, R) 때 사용
* **PC(Program Counter)**


## Register Naming Convention
* R0~R31
* R0: $zero constant 0
* R2~R7: function call
    * R2~R3: return
    * R4~R7: parameters, arguments
* **R8~R25**: user가 assembly language를 쓸 때 사용


## Memory Structure
* **Byte addressable**
    * 주소를 갖고있는 최소 단위가 byte
    * **1 address = 8 bits**
* **Word addressable**
    * 잘 보이지 않고 쓰이지 않음
    * **1 word가 갖는 bits는 컴퓨터마다 다름(MIPS:  32bits)**
    * word마다 주소를 줌
* MIPS에서는 byte마다 주소를 가지고 있음 1word = 32bits = 4bytes
    * 0~3: word0
    * 4~7: word1

## MIPS Design Principles

### 1. Simplicity favors Regularity
* Most of arithmetic/logic instructions have **3 operands**
    * 순서는 고정(destination first)
* Ex)
    * MIPS: ADD C, A, B (C = A+B)
    * MIPS: SUB C, A, B (C = A-B)

### 2. Smaller is faster
* arithmetic/logic instructions 의 경우 register를 사용 (register addressing mode)
* Ex)
    * MIPS: add $s0, $s1, $s2
* **MIPS: only 32 registers (limited)**
    * register의 개수가 늘어남 -> hardware가 복잡 -> propagation delay ↑ -> clock cycle time ↑

### 3. Make common case fast
* Constants는 꽤 자주 operands로 쓰인다.
* Ex)
    * MIPS: A = A+1, B = A - 5
* Sol1) 메모리에 할당 and load from memory
    * Memory access: 시간이 오래 걸림
    * 많이 안쓰이는 상수에 대해 고려
* Sol2) 자주 쓰는 register만 create hard-wired register
    * R0 = $zero = constant 0
* **Sol3) instruction안에 넣는 방법 (Immediate addressing mode)**
    * MIPS: ADDI $3, $3, 1 (A= A+1)
    * 작은 상수를 instruction 안에 두면 메모리에서 프로세서로 실행하기 위해 load
    * **메모리에 두는 것보다 더 빨리 access**
    * register의 낭비 감소

### 4. Good design demands a compromise
* Machine language structure:
    * Length: 32bits (Design Principle 1)
    * **R-type format**<br/>
      <img width="494" alt="스크린샷 2022-09-27 오후 11 53 45" src="https://user-images.githubusercontent.com/63464299/192565527-1a872948-bdf2-4d42-8fe4-76953b9c3384.png">
    * ADD $t0, $s1, $s2
        * $t0 -> rd = R8
        * $t1 -> rs = R17
        * $t2 -> rt = R18
        * ADD -> op, funct(0,32) 
    * 문제점: 
        * LW, SW, ADDI 
        * 1000 -> 2^10 -> 10bits 필요 (표현불가)
    * **I-type format**: for Immediate value<br/>
      <img width="511" alt="스크린샷 2022-09-27 오후 11 59 38" src="https://user-images.githubusercontent.com/63464299/192565575-d6c11cd8-a177-475d-9ec0-27d19d640cfa.png">
    * ADDI $s0, $s1, 4
        * $s0 -> rt = R16
        * $s1 -> rs = R17
        * ADDI -> op = R8
        * 4 -> constant 
