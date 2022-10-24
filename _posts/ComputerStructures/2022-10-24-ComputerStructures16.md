---
layout: single
title: Ch 4. The Processor - (2)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 2. Building Datapath

배워볼 내용: **single clock cycle datapath**
* instuction이 one clock cycle에서 실행
* datapath는 MIPS instruction set에 의해 결정

-----------

# MIPS
* instructions
    * memory-reference instructions
        * lw, sw
    * arithmetic-logical instructions
        * add, sub, and, or, slt
    * control flow instructions
        * beq
* Generic Implementation
    * instruction fetch
        * instruction 주소를 공급하기 위해 PC 사용
        * memory로부터 instruction을 get
    * instruction execute
        * registers를 읽어오기
        * 다음 액션을 결정하기 위해 instruction 사용

## add Operation
* add rd, rs, rt
* RTL(Register Transfer Language) Description
	```
	IR ← mem[PC];
	R[rd] ← R[rs] + R[rt];
	PC ← PC + 4;
	```
	> Fetch instruction from memory<br/>
	> **ADD operation**<br/>
	> Calculate next address

## sub Operation
* sub rd, rs, rt
* RTL Description
	```
	IR ← mem[PC];
	R[rd] ← R[rs] + ~R[rt] + 1;
	PC ← PC + 4;
	```
	> Fetch instruction from memory<br/>
	> **SUB operation** (**two’s complement**)<br/>
	> Calculate next address

## lw Operation
* lw rt, rs, imm16
* RTL Description
	```
	IR ← mem[PC];
	Addr ← R[rs] + SignExt (imm16);
	R[rt] ← Mem[Addr];
	PC ← PC + 4;
	```
	> Fetch instruction from memory<br/>
	> Compute memory address (**Sign Extension**)<br/>
	> **Load data into register**<br/>
	> Calculate next address

## sw Operation
* sw rt, rs, imm16
* RTL Description
	```
	IR ← mem[PC];
	Addr ← R[rs] + SignExt (imm16);
	Mem[Addr] ← R[rt];
	PC ← PC + 4;
	```
	> Fetch instruction from memory<br/>
	> Compute memory address (**Sign Extension**)<br/>
	> **Store data into memory**<br/>
	> Calculate next address

## beq Operation
* beq rt, rs, imm16
* RTL Description
	```
	IR ← mem[PC];
	Cond ← R[rs] + ~R[rt] + 1;
	PC ← Cons ? PC + 4;
		     : PC + 4 + (SignExt(imm16) << 2)
	```
	> Fetch instruction from memory<br/>
	> Compute conditional ‘Cond’ (**two’s complement**)<br/>
	> Fall through if non-zero ‘Cond’<br/>
	> **Branch if zero** ‘Cond’  
