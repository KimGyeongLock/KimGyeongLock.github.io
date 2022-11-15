---
layout: single
title: Ch 4. The Processor - (9)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 9. RISC vs CISC

* Instruction set
    * machine language programs을 구성
    *  CPU의 구조를 결정

---------

# CISC
* Complex Instruction Set Computer
* Goal
    * high-level langauge로 쓴 statement 하나 당 instruction 하나씩 대체 -> Instruction 감소
    * compiler 간소화, 성능 향상
* Major characteristics
    * 많은 instructions
    * 많은 addressing modes
        * -> complex hardware -> 계산이 느려짐
    * instruction format의 가변적인 길이
        * short register addressing mode instruction
        * long direct addressing mode instruction
        * -> 길이가 달라 정렬되지 못함 -> special decoding circuits 필요
    * 메모리에서 operands를 조작하는 instruction
        * instruction 하나 실행할 때마다 memory를 access -> 시간이 오래 걸림

--------

# RISC
* Reduced Instruction Set Computer
* instruction set을 간소화하여 execution time 감소
* Major characteristics
    * 상대적으로 instructions이 적음
    * 상대적으로 addressing mode가 적음
    * load와 store instruction으로 메모리 access 제한
        * CPU안에 많은 registers
        * Overlapped register window (procedure call & return 속도업)
    * 대부분 operations은 레지스터 안에서 끝남
        * execution time이 빠름
        * 대부분 instructions은 simple register addressing mode
    * 고정된 길이, 쉽게 decoded instruction format
        * word boundary에 정렬
        * 간단한 control logic
    * Hardwired 가 micro-programmed control보다 빠름
    * clock cycle 하나당 한 instruction (pipelining)
