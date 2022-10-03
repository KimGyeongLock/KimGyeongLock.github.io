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
* $a0 ~ $a3 : 파라미터를 전달하기 위한 인수
* $v0 ~ $v1 : 반환 값
* $ra: 반환 주소

## MIPS Instruction Pair for Procedures
* Procedure Call
    * JAL ProcedureAddr(Label)
        * main에서 function을 call할 때
        * PC ← ProcedureAddr
        * $ra ← next instruction address (PC)
    * JR $ra
        * function에서 return 할 때
        * PC ← $ra

## Procedures use More Registers by Stack
* more registers → reserved & restored → Stack
* Stack Pointer($SP register in MIPS)
    * 스택에서 가장 최근에 할당된 장소를 point
* PUSH: put data in stack
* POP: get data in stack
* Ex
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
