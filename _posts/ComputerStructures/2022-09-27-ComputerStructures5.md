---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(4)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Introduction to Instruction Set Architecture
# - Instruction Set Completeness

## Instruction Set Completeness
* **Completeness**
    * A computer should have a set of instructions so that the user can construct machine language programs to evaluate any function that is known to be computable  : 계산 가능하다고 알려진 어떤 function이든 제대로 판단할 수 있는 machine language program을 구현할 수 있도록 instruction set을 잘 만들어야 한다.
    * 반드시 있어야 하는 Instructions
        * **Arithmetic / Logical**
        * **Data Transfer (including I/O)**
        * **Control Transfer**
* **Instruction Orthogonality**
    * 똑같은 기능을 하는 instruction가 여러 개 있어도 불필요하다


## Instruction Types

### Arithmetic / Logic Instructions (Data Operations)
* Data Values 수정
* Integer arithmetic operations
    * ADD/Subtract
    * Multiply
    * Divide
    * Increment(++)/Decrement(−−) 필수x
* Logical operations
    * Bitwise AND (&)
    * Bitwise OR ( | )
    * Complement
        * 2진수의 음수표기
        * 1’s complement
            * 3: 0011 => 1100(invert) (-3)
        * 2’s complement
            * 0011 => 1100+1 => 1101
* Shift instructions
    * Logic shift (빠진 자리를 0으로 채움)
        * 0110 -> 1100
    * Arithmetic shift (left shift = ×2, right shift = ÷2)
        * 00110(6)-> 01100(12), 00110(6) -> 00011(3)
    * Rotate(Circular Shift) (빠진 자리를 빠진 숫자로 채움)
        * 1100 -> 1001
* Floating point arithmetic operations

#### CISC vs RISC
* CISC(Complex Instruction Set Computer)
    * instruction set을 복잡하게
    * Increasing functionality 다양한 instruction을 가짐으로 성능을 높임
    * instruction 종류는 많되 high-level language 쓴 거를 compile 했을 때 assembly langauge의 instruction의 개수는 감소
    * 단점: more op code bits and hardware -> propagation delay  <br/> -> clock period가 길어짐 <br/> -> 수행시간이 오래걸림 <br/> -> 하나의 instruction을 실행하기 위해 clock이 더 필요
* RISC(Reduced Instruction Set Computer)
    * cisc의 문제점을 줄임
    * instruction set을 간단히 함으로서 성능을 높임
공통 goal: 성능이 좋은 컴퓨터를 만드는 것

### Data Transfer Instructions
* 다른 곳으로 Data 이동(복사?)
* Load Data (Memory -> processor)
    * lw(load word), lb(load byte)
    * Memory -> register 
* Store Data (processor -> Memory)
    * sw(store word)
    * Register -> memory
* Move data within processor
    * Copy (register -> register)
* Special Instructions (write, output, with ..)
    * I/O Device ↔︎ Processor
    * Block transfer of data
        * Memory ↔︎ Memory
        * Memory ↔︎ I/O Device
* Memory mapped I/O
    * I/O device에 명령을 내리기 위해 device를 특정하는 방법
        * special I/O instructions
        * memory-mapped I/O
    * instruction의 종류를 늘리지 말고 memory address에 I/O Devices를 할당<br/>
    <img width="428" alt="스크린샷 2022-09-27 오후 8 38 27" src="https://user-images.githubusercontent.com/63464299/192517407-0bd304ba-00d0-44d5-96d0-8e4959d52f47.png">


### Control Transfer Instructions (Program Control)
* Jump or Branch(bne, beq): If, While function
* Conditional Branch instructions
    * ex) BEQ A, B, C
* Unconditional Branch instructions
    * ex) Jump A
* Subroutine(function) Calls and returns instructions
* Software interrupt instructions
* (Hardware Interrupts)
* Halt instructions to stop

