---
layout: single
title: Ch 4. The Processor - (3)
toc: true
toc_sticky: true
categories: Structure
published: true
---

3. A Simple Implementation Scheme

# Operation/Instruction Format Summary
* Add, sub, and, or
	* add rd, rs, rt
	* and rd, rs, rt
* Load, store
	* lw rt, rs, imm16
	* sw rt, rs, imm16
* Branch
	* beq rs, rt, imm16

---------

# R-type + (Load or Store) + Branch + PC
<img width="635" alt="스크린샷 2022-11-02 오후 5 09 11" src="https://user-images.githubusercontent.com/63464299/199511472-9a74cdd0-683b-48d5-a8f9-1f66623f319c.png">

---------

# Detailed Design of Control
* Control Signal Types
	* 수행할 operations 선택(ALU, read/write…)
	* 데이터 흐름 제어 (selecting multiplexer inputs)
* instruction의 32bits -> information
* ALU opearation: op.code + function code

## ALU Control
<img width="481" alt="스크린샷 2022-11-02 오후 7 33 26" src="https://user-images.githubusercontent.com/63464299/199511551-d6c3bbb9-f92a-4dd1-af6e-8d1e3632992e.png">

* output: 4-bit ALU control input
	* 0010: ADD
	* 0110: SUB
* input: 
	* **ALUop**
		* 00 = lw, sw = need ‘add’ op
		* 01 = beq = need ‘sub’ op
		* 10 = arithmetic = 
	* function code

|Instruction<br/>opcode|Function<br/>field|Instruction<br/>Operation|ALUOp|Desired<br/>ALU action|ALU<br/>control<br/>Input|
|:---:|:---:|:---:|:---:|
|LW|XXXXXX|load word|00|add|0010
|SW|XXXXXX|store word|00|add|0010
|Branch equal|XXXXXX|branch equal|01|subtract|0110
|R-type|100000|add|10|add|0010
|R-type|100010|subtract|10|add|0110|
|R-type|100100|AND|10|and|0000|
|R-type|100101|OR|10|or|0001|
|R-type|101010|set on less than|10|set on less than|0111|

----------

# A Single Clock Implementation
= A simple Cycle Implementation
= 모든 instructions는 one clock cycle에 실행
= 한 instruction에 한 resource만 사용
= instruction Memory과 data Memory의 분리 & several adders 필요

----------

# R-format instructions dataflow
* add, sub, and, or, slt instructions
<img width="864" alt="스크린샷 2022-11-02 오후 8 02 25" src="https://user-images.githubusercontent.com/63464299/199511948-bc053863-faa8-4b4d-84b3-1285d5acdc70.png">
* RegDst: 1 (to select Rd)
* RegWrite: 1 (to enable writing Rd)
* ALUSrc: 0 (to select Rt value from register file)
* ALUOp: Dependent on operation
	* add: 0010
	* sub: 0110
	* slt: 0111
	* and: 0000
	* or: 0001
* MemWrite: 0 (to disable writing memory)
* MemRead: 0 (to disable reading memory)
* MemtoReg: 0 (to select ALU output to register)
* PCSrc: 0 (to select next PC)

----------

# I-format instructions dataflow
## Load
<img width="846" alt="스크린샷 2022-11-02 오후 9 34 59" src="https://user-images.githubusercontent.com/63464299/199517097-e63984af-a126-4701-b248-86b5f1922bf7.png">
* RegDst: 0 (to select Rt)
* RegWrite: 1 (to enable writing Rt)
* ALUSrc: 1 (to select immediate field value from instruction)
* ALUOp: add
* MemWrite: 0 (to disable writing memory)
* MemRead: 1 (to disable reading memory)
* MemtoReg: 1 (to select memory output to register)
* PCSrc: 0 (to select next PC)

## Store
<img width="846" alt="스크린샷 2022-11-02 오후 9 34 59" src="https://user-images.githubusercontent.com/63464299/199512138-cff37336-6d8d-438f-b6ab-5d73b3879ca5.png">
* RegDst: X (don’t care)
* RegWrite: 0 (to disable writing a register)
* ALUSrc: 1 (to select immediate field value from instruction)
* ALUOp: add
* MemWrite: 1 (to enable writing memory)
* MemRead: 0 (to disable reading memory)
* MemtoReg: X (don’t care)
* PCSrc: 0 (to select next PC)

## Beq
<img width="844" alt="스크린샷 2022-11-02 오후 9 36 05" src="https://user-images.githubusercontent.com/63464299/199512520-3a61e283-d06a-4604-bcf2-6f66a60a8431.png">
* RegDst: X (don’t care)
* RegWrite: 0 (to disable writing a register)
* ALUSrc: 0 (to select Rt value from register file)
* ALUOp: sub
* MemWrite: 0 (to disable writing memory)
* MemRead: 0 (to disable reading memory)
* MemtoReg: X (don’t care)
* PCSrc: zero AND branch

------------

# Our Single Cycle Control Structure
* All of the logic is combinational 
	* PC, Reg 제외, Memory는 보류(5장)
* ALU는 바로 right answer를 만들지 못함
	* propogation delay로 인해 어느정도 시간이 흐른 뒤에 state element2 앞에 나타남
	* clock이 뛰어야 State element2에 값이 저장
* clock과 write signal로 write를 결정
* Cycle time은 Longest path(critical path)의 길이의 결정
	* clock period > critical path

------------

# Single Cycle Implementation Performance
* memory (200ps)
* ALU and adders (100ps)
* register file access(50ps)

<img width="675" alt="스크린샷 2022-11-02 오후 10 59 32" src="https://user-images.githubusercontent.com/63464299/199512704-009adac1-c2b1-4b04-93c4-2bac4378b323.png">
* Clock Cycle time with single clock: longest instruction = 600ps
	* clock period = 최소 600ps
* CPI = 1
	* Clock cycle Per Instruction = single clock cycle = 1
* Execution Time = #instruction * CPI * Clock Cycle Time = #instruction  * 600ps

------------

# Single Cycle Problems
* floating point 같은 복잡한 instruction
* chip area의 낭비
	* Add ALU 낭비
* Solution
	* cycle time smaller
	* clock period smaller
	* different instructions은 different numbers of cycles를 가짐
	* => **Multicycle datapath**
