---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(3)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# - Addressing modes
* operand가 메모리나 레지스터에 있는 장소를 지정하는 다양한 방법
* Advantages
    * 프로그래밍 다양성
        * pointers to memory
        * counters for loop control
        * indexing of data
    * addressing field의 비트 수 감소
* **Effective Address(E.A.)**
    * Actual address of the location containing the referenced operand
    * Ex) \[In ARM\]  LDR(Load cpu의 register) r1, [r2, #20]
        * <img width="592" alt="스크린샷 2022-09-14 오후 12 48 18" src="https://user-images.githubusercontent.com/63464299/190156153-f3ef6bc6-da03-4e74-968a-9c510f079f4e.png">{: width="350" height="350"}
        * Effective Address: 120
        * #: 값 자체, 날 것 그대로의 데이터
    * Ex) \[In MIPS\]  lw(load word) $t1, 1000($s1)
        * <img width="601" alt="스크린샷 2022-09-14 오후 8 16 28" src="https://user-images.githubusercontent.com/63464299/190156160-1e9df0c9-6359-408a-8a17-de849033c2b0.png">{: width="350" height="350"}
        * Effective Address: 1100
        * $: register

## Type 

1. **Implied** addressing mode 
	* No explicit address
	* 명령어 실행에 필요한 operand를 지정하지 않아도 묵시적으로 수행하는 방식
	* Ex) PUSH A, ADD A, RTS 
	
2. **Immediate** addressing mode(즉시 주소 지정 방식)
	* Operand field contains the actual operand value 
	* operand에 연산에 필요한 숫자 데이터를 직접 넣어주는 방식
	* 명령어 자신이 데이터를 직접 포함하고 있어 명령어의 실행이 바로 이루어지는 방법
	* ex) \[In ARM\] ADD r3, r3, #4
	  * r3←r3+4
	* ex) \[In MIPS\] addi $s1, $s2, 4
		* s1←s2+4
		* **addi**(immediate address): address랑 다름
		
3. **Register** addressing mode
	* Selected Register contains the operand
	* E.A. = Selected Register
	* Ex) \[In ARM\] ADD r0, r1, r2 ( r0←r1+r2)
		* r1, r2 register안에 operand가 포함
4. **Register Indirect** addressing mode
	* Selected Register contains the address of operands
	* E.A. = Contents of Selected Register
	* Ex) MOVE.W (A1), D1
		* IF) A1(address): 1000<br/>
		 	Memory에서 1000번지를 찾아 a value를 D1(Data)에 Load
5. **Direct** Addressing mode
	* Effective address is equal to the address part of the instruction and operands reside in memory
	* E.A. = Address Field of Instruction
	* Ex) MOVE.W 10000, D1
		* Memory에서 10000번지를 찾아 a value를 D1(Data)에 Load
6. **Indirect** Addressing mode
	* The Address field gives the address where the effective address is stored
	* E.A. = Memory[Address Field of Instruction]
	* Two Memory References (Slowest)
	* Ex) ADD (1000)
		* Memory에서 1000번지 주소로 감, 주소값이 들어있다면 다시 2000번지로 이동
		   <br/> 2000번지 value를 add
7. **(PC) Relative Address** mode
	* PC(Program Counter): 다음에 실행될 instruction의 주소를 포함
	* Value in PC is added to the address part of instruction to obtain the effective address (branch type instructions)
	* E.A. = PC + Offset in Address Field of Instruction(Operands)
	* \[In MIPS\]<br/>
		100     bne $s0, $s1, Exit // Code:Exit<br/>
    104     add . . .<br/>
		108     sub . . .<br/>
		112     lw  . . .<br/>
		116   Exit: . . . // Label:Exit<br/>
		* bne: Branch(jump) (if)Not Equal → if($s0≠$s1) Exit // beq(Branch (if)E Qual)
		* PC ←104 // bne instruction 전에 다음 실행될 instruction의 주소가 미리 들어가있음
		* Exit(Label)’s address: 116
		* E.A. = (PC) + Exit = 104 + **3***4 = 116
			* Exit = 3 으로 Translate // Exit(Code)와 Exit(Label) 사이에 3개의 instruction

### Direct vs. Indirect
Indirect
* 장점: address field can be extended to word length
* 단점: slower

### Direct vs. Register
Register
* faster / cpu안에 register가 있어 메모리로 갈 필요가 없음<br/>
Direct
* addressing space of memory is larger / cpu 안의 register는 다소 제한

