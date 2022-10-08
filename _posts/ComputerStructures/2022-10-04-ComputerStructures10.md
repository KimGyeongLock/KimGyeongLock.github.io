---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(9)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 6. Supporting Procedure Call

## Procedure Call Steps
1. Procedure이 접근할 수 있는 곳에 파라미터 배치
2. Procedure로 control transfer
3. Procedure에 필요한 storage resources 확보
4. 원하는 작업 수행
5. calling program이 접근할 수 있는 곳에 결과값을 배치
6. 원래 지점으로 control return

## MIPS Registers for Procedure Call
* **$a0 ~ $a3** : 파라미터를 전달하기 위한 인수
* **$v0 ~ $v1** : 반환 값
* **$ra**: 반환 주소

## MIPS Instruction Pair for Procedures
* **Procedure Call**
    * **JAL** ProcedureAddr(Label)
        * main에서 function을 call할 때
        * PC ← ProcedureAddr
        * $ra ← next instruction address (PC)
    * **JR** $ra
        * function에서 return 할 때
        * PC ← $ra

## Procedures use More Registers by Stack
* more registers → reserved & restored → Stack
* **Stack Pointer($SP register in MIPS)**
    * 스택에서 가장 최근에 할당된 장소를 point
* PUSH: put data in stack
* POP: get data in stack
* Ex)
	```
	int leaf_example(int g, int h, int i, int j) {
		int f;
		f = (g+h) - (i+j);
		return f;
	}
	```
    1. Save registers in Stack
        * Parameters in $a0~$a3
            * $a0 = g, $a1 = h, $a2 = i, $a3 = j
        * Return address is in $ra
            * $ra = PC
        * Reserve $s0, $t0, $t1 in stack(PUSH)
            * $s0 = f, $t0 = g+h, $t1 = i+j
    2. Compute f = (g+h) - (i+j)
    3. Place the return values in $v0
        * $v0 = f
    4. Restore register values
        * Restores $s0, $t0, $t1 from stack(POP)
    5. Return control to caller by JR $ra

## MIPS Software Convention on Registers

* Reducing the Register Spiling 
    * **Register Spiling**: register 값을 메모리에 save 
    * **$t0 ~ $t9**
        * function 이후 사용하지 않을 register -> save할 필요없음
        * ~~sw $t0, 8($sp)~~
    * **$s0 ~ $s7**
        * function 이후에도 사용할 register -> save 필요
        * sw $s0, 4($sp)
    * => save time


## Nested Procedure Call
= recursion
* C language<br/>
  ```
  int fact (int n) { 
	if (n < 1) 
		return 1; 
	else 
		return (n * fact (n-1)); 
	} 

       ```
* MIPS<br/>
  ```
  fact : 
	addi $sp,$sp,-8 # adjust stack for 2 items($ra, $a0) 
	sw $ra, 4($sp) # saves return address 
	sw $a0, 0($sp) # saves argument n
	slti $t0, $a0,1 # if n < 1, $t0= 1, otherwise $t0 =0
	beq $t0,$zero, L1 # if n >= 1 goto L1 
	addi $v0,$zero,1 # if n < 1, return 1
	addi $sp,$sp,8 # pop 2 items($ra, $a0)
	jr $ra # return to after jal
  L1:   addi $a0,$a0, -1 # n=n-1
	jal fact # recursive call with (n-1) 
	lw $a0, 0 ($sp) # return from jal : restore n 
	lw $ra, 4 ($sp) # restore address
	addi $sp,$sp,8 # adjust stack for 2 items 
	mul $v0, $a0,$v0 # return n * fact(n-1) 
	jr $ra # return to the caller
  ```

## Allocating Space for New Data on the Stack
* **Procedure frame**(Active record)
    * function이 call할 때마다 생성
    * 함수에 저장된 registers와 local variables을 포함하는 stack을 위한 segment
    * **$fp register(Frame Pointer)**
        * Procedure frame의 첫번째 word를 가르킴
        * 지역 변수에 대한 안정적인 참조를 위한 기반을 제공


## Memory Layout
* Text: program code
* Static data: global variables
* Dynamic data: heap
* Stack: automatic storage
