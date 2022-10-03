---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(8)
toc: true
toc_sticky: true
categories: Structure
published: true
---


# 5. MIPS Instruction Format & Addressing Modes

Machine Language Structure (MIPS)
* Represent: 0/1 (binary code)
* Length: 32 bits (Design Principle 1)
* Formats: **3 types**


## R-type Instruction Format
* for arithmetic and logic instructions

<img width="511" alt="스크린샷 2022-10-03 오후 4 04 15" src="https://user-images.githubusercontent.com/63464299/193522820-5fd866f2-10de-4910-a525-54b5b9cfce91.png">
* 모든 R-type instruction, op code = 0
* function code: operation 구분(ADD, SUB..)

## I-type Instruction Format
* for immediate value(constant value or address)
* LW, SW, ADDI

<img width="511" alt="스크린샷 2022-10-03 오후 4 06 36" src="https://user-images.githubusercontent.com/63464299/193522881-97922cb9-656d-4f5a-b263-6983ab6e537b.png">


## J-type Instruction Format
* 16bits보다 더 필요
* J, JAL

<img width="570" alt="스크린샷 2022-10-03 오후 4 15 06" src="https://user-images.githubusercontent.com/63464299/193522927-c5475ce4-fdd9-46e2-9938-479d39abcbd5.png">
* PC\[31:28\] 4bits
    * 고정
* PC\[27:2\] 26bits
    * 직접 Label이 있는 곳의 위치 언급(주소값)
* PC\[1:0\]
    * MIPS - byte addressable
    * 1 word = 4 bytes
    * x4 = << 2 (left shift)

## Op-code & Function 표
![page55image44325584 복사본](https://user-images.githubusercontent.com/63464299/193522969-c762ca83-2758-4ab0-ac39-afe155335eb8.jpeg)<br/>
<br/>
![page55image443255ee](https://user-images.githubusercontent.com/63464299/193523018-61faced0-c7df-465d-9376-326a232b338b.jpeg)

## Stored Program Concept
* 폰 노이만 아키텍쳐
* Two Principles
    * Instructions are represented as numbers(0/1)
    * Programs(Instruction sets) are stored in memory
* Memory에서 숫자(0/1)로 되어 있는 Instructions를 한 문장씩 Processor에 가져가 실행

### Fetch & Execute Cycle
* **Fetch**: Memory에서 Processor로 instructions의 이동
    * 정확히는 Processor 안의 Instruction Register(IR)로 이동
* Register 안에 있는 Content에 따라 다음 액션을 control
* 다시 다음 instruction을 fetch (Cycle)
* Control Transfer Instructions
    * control flow 바꿈
    * 실행해야 할 다음 instruction 변경
    * → **PC register** 
        * 다음 instruction이 있는 메모리 위치를 point

## LUI
* LUI (Load Upper immediate instruction)
    * Breaking large constants into pieces and then reassemble them into a register

<img width="540" alt="스크린샷 2022-10-03 오후 6 50 59" src="https://user-images.githubusercontent.com/63464299/193609119-057f35c2-8221-49c3-a6f3-99483407f587.png">

* Ex) 32-bit constant “0x003D 0900”
    * LUI $t0, 0x003D -> t0: 003D 0000
    * ORI $s0, $t0, 0x0900 -> s0: 003D 0900
    * 재조립시 upper part 16bits 판단 방법 (???? 0900)
* Sign Extension
    * Arithmetic
    * addi $s1, $t0, 0x000f -> sign bit = 0, 16bits 모두 0
    * addi $s, $t0, -4 -> sign bit = 1, 16bits 모두 1
* Zero Extension
    * Logic
    * 16bits 모두 0

## Pseudo Instruction
* Pseudo instruction
    * 원래  MIPS instruction set 안에는 없는데 assembly language로 쓰면은 마치 있는 것처럼 취급을 해서 action
* Copy 
    * Move $t0, $t1
        * = add $t0, $t1, $zero
* Branch if Less Than
    * BLT $t0, $t1, L
    * if ($t0 < $t1) goto L
        * = slt $at, $t0, $t1<br/>bne $at, $zero, L
* Branch if Greater Than
    * BGT $t0, $t1, L
    * if ($t0 > $t1) goto L
* Branch if Greater (Less) Than or Equal to
    * BGE $t0, $t1, L
    * if ($t0 >= $t1) goto L


## MIPS Addressing Modes
1. Immediate addressing
    * addi, andi, slti
    * I-Type
2. Register addressing
    * add, mud, and, slt, sll
    * R-Type
3. Base addressing
    * lw, sw
4. PC-Relative addressing
    * beq, bne
5. Pseudo-direct addressing
    * j, jal
    * direct addressing mode와 비슷하지만 똑같지X


## Spim
**Pseudo Assembly Instruction**
* **li** $rs, immediatamente: Load immediate value(immed) to $rs
* **la** $rs, addr: Load address(addr) to $rs

**System call (syscall)**
* consol window에 **출력**을 하거나 **입력**을 받을 때 사용
* 하고 싶은 action을 $v0 register에 load
    * li $v0, 4
    * li $v0, 1
        * 4: print String 
        * 1: print Integer
* $a0 ~ $a3: load argument (floating-point: $f12)
    * la $a0, str
    * la $a0, 5

