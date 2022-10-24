---
layout: single
title: Ch 4. The Processor - (1)
toc: true
toc_sticky: true
categories: Structure
published: true
---

Two Types of Implementation Components
* Combinational
    * same input -> same output
    * output = f(input)
    * ALU, Adder, MUX
        * AND, NAND, OR, NOR, XOR, NOT
* Sequential
    * same input -> possibly different output
    * output = f(input, current state)
    * memory, registers

## State Elements
* Unclocked vs Clocked (Asynchronous vs Synchronous)
    * Synchronous: clock의 기준에 따라 움직임이 제어
    * Asynchronous: 기준이 없어 분석이 어려움
* Clocks used in synchronous logic - edge triggered (vs. master-slave)
    * state를 포함한 element (Flip-Flop)이 언제 업데이트 되는냐? -> clock에 따라
    * **rising edge**(positive edge) 
        * clock signal : 0 -> 1
        * rising edges 사이 간격 : **Cycle time**
    * **falling edge**(negative edge) 
        * clock signal : 1 -> 0

## D-latch
* Two inputs
    * D: data value
    * C: clock signal
* Two outputs
    * Q, Q-(bar)
    * output은 clock signal이 active할 때만 수행
    * clock이 0->1일 때 D값이 Q에 나타남

## D flip-flop
latch의 문제점을 보완-> latch를 2개 붙여 flip-flop을 만듦 (master-slave flip-flop)
clock이 1->0일때 D값이 Q에 나타남 (like negative edge flip-flop)
ones(zeros) catching problem -> Edge-triggered flip-flop 사용

