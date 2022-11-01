---
layout: single
title: Ch 4. The Processor - (1)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Review
# Logic design review

## Two Types of Implementation Components
* **Combinational**
    * Elements that operate on **data values**
    * same input -> same output
    * **output = f(input)**
    * ALU, Adder, MUX
        * AND, NAND, OR, NOR, XOR, NOT
* **Sequential**
    * Elements that **contain state**
    * same input -> possibly different output
    * **output = f(input, current state)**
    * **Memory, Register**
        
## State Elements
* Unclocked vs Clocked (**Asynchronous** vs **Synchronous**)
    * **Synchronous**: clock의 기준에 따라 움직임이 제어
      * Clocks - edge triggered 
      * clock에 따라 element 업데이트
      * **rising edge**(positive edge) 
         * clock signal : 0 -> 1
         * rising edges 사이 간격 : **Cycle time**
      * **falling edge**(negative edge) 
         * clock signal : 1 -> 0
    * **Asynchronous**: 기준이 없어 분석이 어려움
   
## D-latch
* Two inputs
    * D: data value
    * C: clock signal
* Two outputs
    * Q, Q-(bar)
    * output은 clock signal이 active할 때만 수행
    * clock이 0->1일 때 D값이 Q에 나타남

## D flip-flop
* clock edge에서만 output이 변경
* **Master-slave flip-flop**
    * latch의 문제점을 보완-> latch를 2개 붙여 flip-flop을 만듦 
    * clock이 1->0일때 D값이 Q에 나타남 (like negative edge flip-flop)
    * ones(zeros) catching problem -> Edge-triggered flip-flop 사용

## Edge-triggered flip-flop
* 일부 state elements의 내용 Read
* 일부 combinational logic을 통해 값 Send
* 하나 이상의 state elements에 결과를 작성


