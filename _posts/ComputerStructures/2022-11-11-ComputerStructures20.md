---
layout: single
title: Ch 4. The Processor - (6)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# Basic Pipeline
* Single Clockcycle datapath와 유사
    * I-memory, D-memory 분리
    * ALU 여러개
    * Harvard Architecture
        * 각각 다른 instructions가 각각 다른 stages에 동시에 존재
        * resources가 여러 곳에서 동시에 필요
* datapath를 단계로 나누기 위해서 필요한 것
    * 구간마다 register로 값을 저장하여 다음 단계에 전달(Multi Clockcycle datapath)
    * -> 문제점: LW instruction - Write register address의 손실
    * -> 해결: Write register address를 다음 단계 register로 계속 넘겨줌

# Pipeline Control
* Instruction Fetch and PC Increment 
    * nothing special to control
    * instruction에 관계없이 실행
* Instruction Decode / Register
    * no optional control
    * instruction에 관계없이 실행
* Execution
    * RegDst
    * ALUOp
    * ALUSrc
* Memory Stage
    * Branch
    * MemRead
    * MemWrite
* Write Back
    * MemtoReg
    * RegWrite

<img width="625" alt="스크린샷 2022-11-11 오후 1 19 01" src="https://user-images.githubusercontent.com/63464299/201262915-946d49f7-7ea9-43b7-b09b-fba9ee2c9684.png">

