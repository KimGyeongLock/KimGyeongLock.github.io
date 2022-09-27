---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(3)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Introduction to Instruction Set Architecture
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

### 1. **Implied** addressing mode 
* No explicit address
* 명령어 실행에 필요한 operand를 지정하지 않아도 묵시적으로 수행하는 방식
* Ex) **PUSH A**, **ADD A**, RTS 
	
### 2. **Immediate** addressing mode(즉시 주소 지정 방식)
* Operand field contains the actual operand value 
* operand에 연산에 필요한 숫자 데이터를 직접 넣어주는 방식
* instruction이 데이터(operand)를 직접 포함하고 있어 명령어의 실행이 바로 이루어지는 방법
* 장점: 빠르다
* 단점: 수의 크기에 제한
* ex) \[In ARM\] ADD r3, r3, **#4**
  	* r3←r3+4
* ex) \[In MIPS\] addi $s1, $s2, **4**
	* s1←s2+4
	* **addi**(immediate address): address랑 다름
	
![21310A36576092BF35](https://user-images.githubusercontent.com/63464299/190400084-d50080ac-a11a-4fd4-b874-99867b77ffac.jpeg)

### 3. **Register** addressing mode
* Selected Register contains the operand
* address part는 memory가 아닌 **Register**를 Point
* **operands는 register에 위치**
* **E.A. = Selected Register**
* 장점: 명령어의 주소필드가 작아도 됨. 메모리 접근x. 매우 빠르다
* 단점: register 개수 제한
* Ex) \[In ARM\] ADD r0, r1, r2 (r0←r1+r2)
	* r1, r2 register안에 operand가 포함
		
![227E9136576092C204](https://user-images.githubusercontent.com/63464299/190403490-8f5b17b1-27e9-44b6-86ee-a77ea7f973d6.jpeg)
	
### 4. **Register Indirect** addressing mode
* Selected Register contains the address of operands
* address part는 **Register**를 Point
* Register는 메모리의 operand의 주소값을 가짐
* **E.A. = Contents of Selected Register**
* 장점: 넓은 주소 공간, 한번의 메모리 접근
* Ex) MOVE.W (A1), D1
	* IF) A1(address): 1000<br/>
	 	Memory에서 1000번지를 찾아 a value를 D1(Data)에 Load
		
![233B4D36576092C232](https://user-images.githubusercontent.com/63464299/190403521-c54e9492-cb5e-49ea-9f82-464923f8a392.jpeg)	
			
### 5. **Direct** Addressing mode
* instruction의 address part는 **Operand의 주소**를 가짐
* **operands는 memory에 위치**
* **E.A. = Address Field of Instruction**
* 단점: 주소 공간 제한
* Ex) MOVE.W 10000, D1 , (or ADD A)
	* Memory에서 10000번지를 찾아 a value를 D1(Data)에 Load
		
![272C1D36576092C034](https://user-images.githubusercontent.com/63464299/190400343-e02ffbc0-d629-425d-88a2-8445a566cad5.jpeg)
	
### 6. **Indirect** Addressing mode
* Instruction의 address field는 **Operand의 주소값(E.A.)을 가지는 곳의 주소**를 가짐
* The Address field gives the address where the effective address is stored
* **E.A. = Memory[Address Field of Instruction]**
* Two Memory References (**Slowest**)
* 장점 : word길이가 n이면 2^n개의 주소 공간
* Ex) ADD (1000) , (or ADD (A))
	* Memory에서 1000번지 주소로 감, 주소값이 들어있다면 다시 2000번지로 이동
	   <br/> 2000번지 value를 add

![26309636576092C135](https://user-images.githubusercontent.com/63464299/190401758-d28484db-5fcb-471d-9046-0c1d4a6885e4.jpeg)
		   
### 7. **(PC) Relative Address** mode
* PC(Program Counter): 다음에 실행될 instruction의 주소를 포함
* Value in PC is added to the address part of instruction to obtain the effective address (branch type instructions)
* **E.A. = PC + Offset in Address Field of Instruction(Operands)**
* \[In MIPS\]<br/>
```
   100         bne $s0, $s1, Exit // Code:Exit
   104         add . . .<br/>
   108         sub . . .<br/>
   112         lw  . . .<br/>
   116   Exit: . . . // Label:Exit
```   
	* bne: Branch(jump) (if)Not Equal → if($s0≠$s1) Exit // beq(Branch (if)E Qual)
	* PC ←104 // bne instruction이 실행될 때 PC는 다음 실행될 instruction의 주소를 가짐
	* Exit(Label)’s address: 116
	* E.A. = (PC) + Exit = 104 + **3***4 = 116
		* Exit = 3 으로 Translate // Exit(Label)과 PC가 포인터하는 곳 사이에 3개의 instruction
		
* <br/>
```
      slt $t0, $s0, $s1 #t0 = 1 if $s0 < $s1
      beq $t0, $zero, Less
      add $s2, $s0, $s1
      j Exit
Less: sub $s2, $s0, $s1
Exit:
```
Convert to machine code<br/>
```
000000 10001 10010 01000 00000 101010 /* slt
000100 01000 00000 00000 00000 000010 /* beq
000000 .............................. /* add
000010 .............................. /* j
000000 .............................. /* sub
```
> Less = 2<br/>
> PC = 208<br/>
> Address of next instruction = PC + 2*4 = 216<br/>
		
#### Memory Structure of ARM and MIPS
* Main Memory(random access memory)
    * 일차원 배열
    * 주소는 배열의 index , 주소를 통해 메모리에 access
* 1 byte 단위마다 메모리 주소를 가짐(bit X)
* 1 word = 4 bytes access
    * ARM, MIPS: 32bits -> 4 bytes
        * 2^32 bytes = 2^30 words(bytes/4) 주소를 표현
    * A[i] = A+i*4 byte address
    	* word0의 대표주소: 0 , word1의 대표주소: 4


### 8. Base Register Addressing mode
* lw instruction에서 사용하는 address mode
* **E.A. = Base Register + Offset in the Address Field of Instruction**
	* offset: 얼마나 떨어져 있는가
* \[In MIPS\]<br/>
```
lw $t1, 1000($s1)
E.A. = (s1) + 1000
```
> memory에서 processor로 값을 load(word size)<br/>
> processor안의 t1 register에 저장<br/>
> 메모리 주소값 계산: processor의 s1 register안에 있는 값+1000

* \[In ARM\]<br/>
```
LDR r5, [r3, #32]
E.A. = (r3) + 32
```

----------

## Direct vs. Indirect
Indirect
* 장점: address field can be extended to word length<br/> word길이가 n이면 2^n개의 주소 공간을 가진다.
* 단점: slower

## Direct vs. Register
Register
* faster / cpu안에 register가 있어 메모리로 갈 필요가 없음<br/>

Direct
* addressing space of memory is larger than register / cpu 안의 register는 다소 제한

