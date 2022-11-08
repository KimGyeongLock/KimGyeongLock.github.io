---
layout: single
title: Ch 4. The Processor - (4)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 4. Multicycle Implementation

# Multicycle Approach
* functional units 재사용
    * ALU: 주소 계산, PC증가
    * Memory: instruction과 data 저장
* **finite state machine** 사용

------------

# Finite State Machine
* A set of states
    * Current state: Flip-Flop
* Combinational logic
    * Next-state function
        * current state와 input에 의해 결정
    * Output function
        * current state와 입력 가능성에 의해 결정
* Moore machine을 사용 (current state에만 기반한 출력)

------------

# MultiCycle Datapath for MIPS - Basic Instructions
* instructions을 단계별로 나누고, 각 단계는 cycle을 가짐
    * 모든 work는 일정하게 균형 (가장 긴 ps를 기준)
    * 각 cycle은 한가지 **major functional unit**만을 제한
        * Memory access, ALU± (Mux X)
* At the end of a cycle
    * later cycles을 위해 값 저장 (가장 쉬운 일)
    * introduce additional internal registers 
        * **Instruction Register**: 메모리에서 instruction을 읽어왔을 때 저장하는 Reg (IR)
        * **Memory Data Register**: 메모리에서 데이터를 읽어왔을 때 저장하는 Reg<br/>(Mem Buffer Reg, MBR, MDR)
        * **A,B**: Read or Store Data
        * **ALUOut**: ALU 값 저장

------------

# Multicycle datapath: Simplecycle datapath와 비교
* **Single Memory**
* **Single ALU**
* **Register 추가(intermediate results저장)**
    * IR
    * A, B
    * ALUOut
    * MDR cf)Memory Address Register
* **More Multiplexer(functional units 공유)**
    * Memory 앞
        * instruction을 불러올 때 PC에 주소를 load (Mux=0)
        * ALUOut에 있는 data의 주소를 사용해서 data를 load (Mux=1)
    * ALU 앞
        * PC +4
            * 윗 Mux: 0(PC)
            * 밑 Mux: 1(4)
        * add
            * 윗 Mux: 0(A)
            * 밑 Mux: 1(B)
        * Branch Target address 계산
            * 윗 Mux: 0(PC)
            * 밑 Mux: 3(Sign extend, Shift left 2)

------------

# Five Execution Steps

## 1. Instruction Fetch
* instruction의 종류에 상관없이 실행
* PC에서 instruction을 가져와서 IR에 넣음
* PC를 4 증가시키고 PC에 다시 넣음
    * ALU가 다른 Step에서는 다른 용도로 쓰일 수 있기 때문에 ALU가 별 다른 일이 없을 때 PC값을 4 증가
* RTL
   ```
   IR <= Memory[PC];
   PC <= PC + 4;
   ```

## 2. Instruction Decode and Register Fetch
* **Decode**: 각 instruction에 따라 각각 다른 control signal을 발생
* 필요한 경우 rs, rt 레지스터를 읽음 (rs는 항상 필요, rt는 경우에 따라)
* instruction이 branch일 경우를 대비하여 branch address를 미리 계산
    * branch가 아니어도 상관X
* RTL<br/>
   beq $t0, $t1, exit<br/>
   ```
   A <= Reg[IR[25-21]];  // $t0
   B <= Reg[IR[20-16]];  // $t1
   ALUOut <= PC + (sign-extend(IR[15-0]) << 2); // PC(PC+4) + exit
   ```
* instruction의 종류에 상관없이 실행
    * control signals이 결정되지 않음

## 3. Execution, Memory Address Computation, or Branch Completion
* **Execution**: R-type instruction(ADD, SUB, AND, OR, SLT)
   ```
   ALUOut <= A op B;
   ```
* **Memory Address Computation**: lw, sw
   ```
   ALUOut <= A + sign-extend(IR[15-0]);
   ```
* **Branch Completion**: Branch - 3단계 끝
   ```
   if (A==B) Pc <= ALUOut;
   ```
   > ALUOut = 2단계에서 계산한 branch target address

## 4. Memory Access or R-type instruction completion
* **Memory Access**: lw, sw  sw-4단계 끝
   ```
   MDR <= Memory[ALUOut]; // LW
         or
   Memory[ALUOut] <= B; // SW
   ```
   > ALUOut = 3단계에서 계산한 memory address
* **R-type instruction completion**: R-type - 4단계 끝<br/>
   ADD $t0, $t1, $t2<br/>
   ```
   Reg[IR[15-11]] <= ALUOut; // $t0
   ```
 	> ALUOut = 3단계에서 계산한 A op B
## 5. Write-back step
* lw - 5단계 끝
   ```
   Reg[IR[20-16]] <= MDR;
   ```
