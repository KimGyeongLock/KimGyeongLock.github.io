---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(7)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 4. MIPS Instruction Set

## 	Arithmetic / Logic instructions
* **Arithmetic Instructions**
    * ADD $s0, $s1, $s2    # $s0←$s1 + $s2
    * ADD**I** $s0, $s1, **100**   # $s0←$s1 + 100
    * SUB $s0, $s1, $s2    # $s0←$s1 - $s2
    * MULT $s1, $s2           # **Hi, Lo**←$s1 * $s2
    * DIV $s1, $s2               # **Hi, Lo**←$s1 / $s2
    * **MFHI** $s1                     # $s1←Hi 
    * **MFLO** $s1                    # $s1←Lo 
    * **MF(Move From)**
* **Logical Instructions**
    * AND $s0, $s1, $s2   # $s0 ← $s1 bitwise-AND $s2
    * OR $s0, $s1, $s2      # $s0 ← $s1 bitwise-AND $s2
    * AND**I** $s0, $s1, **31**    # $s0 ← $s1 bitwise-AND 31
    * ORI $s0, $s1, 32      # $s0 ← $s1 bitwise-OR 32 
    * NOR $s0, $s1, $s2  # $s0 ← $s1 bitwise-NOR $s2
    * **SLL(Shift Left Logic)** $s0, $s1, 10      # $s0 ← $s1 << 10 (shift left logical)
    * **SRL(Shift Right Logic)** $s0, $s1, 10      # $s0 ← $s1 >> 10 (shift right logical) 

## Data transfer instructions
* Data structures은 메모리에 상주
* arithmetic/logic operation은 register에서 발생
* Memory와 Register간의 Data transfer 필요
* register 끼리도 Data transfer 필요
* **MIPS**: Only **two instruction** for **Memory Access**
    * **Load Instruction**(lw, ld..)
        * LW $s1, 8($s0)
            * : $s1 <- Memory\[$s0 + 8\]
            * 4 Bytes \[$s0+8\], \[$s0+9\], \[$s0+10\], \[$s0+11\]
            * if $s0 = 10
            * 18,19,20,21 번지 주소의 값들을 $s1에 불러옴
    * **Save Instruction(sw)**
        * SW $s1, 12($s0)
            * : Memory\[$s0 + 12\] <- $s1
    * **RISC architecture** 특징
* Ex) A[8] = h + A[8]
    * MIPS:<br/>
      ```
      lw $t0, 32($s3)
      add $t0, $s2, $t0
      sw $t0, 32($s3)
      ```
      > $s3: Address of A<br/>
      > $s2: h<br/>
      > 32 = 8 * 4bytes (= word size)
    * Base Register Addressing (\[R\] + Offset)
        * Base Register: $s3
        * Offset: 32

## Control Instructions
* **Conditional** branch instructions
    * **BEQ (Branch if EQual)**
        * BEQ $s1, $s2, label 
        * if ($s1 == $s2) PC = TargetAddress
        * I Type
            * op = 4 
            * 16bits = offset(word count)
    * **BNE (Branch if Not Equal)**
        * BNE $s1, $s2, label 
        * if ($s1 ≠ $s2) PC = TargetAddress
        * I Type  
            * op = 5 
            * 16bits = offset(word count)
    * **SLT (Set Less Than)**
        * SLT $t0, $s1, $s2
        * if ($s1 < $s2) then $t0 = 1 else $t0 = 0
        * R Type
            * op = 0, func = 42
    * **SLTI (Set Less Than Immediate)**
        * SLTI $s1, $s2, 100
        * if ($s2 < 100) then $s1 = 1 else $s1 =0
        * I Type
            * constant = 100
* **Unconditional** branch instructions
    * Jump시 PC는 새로운 값을 설정
    * **J (Jump)**
        * target address로 jump
        * J 1000(label)
        * PC ← 1000
        * J Type
            * op = 2 (6bits)
            * traget address (26bits)
    * **JR (Jump Register)**
        * JR $ra 
        * PC ← $ra
        * R Type
            * op = 0, func = 8
            * rs = 31 ($r1: 31번 Reg)
    * **JAL (Jump And Link)**
        * JAL 1000 
        * $ra ← PC
        * PC ← 1000
        * J Type
            * op = 3
* Control Instruction
    * Beq / Bne $t0, $t1, **16 bit Offset**
        * PC (Target Address) ← PC + Offsetx4
    * J / Jal **26 bit address**
        * PC (Target Address) ← PC(31:28)(4bits) && (address << 2)
        * shift left 2 (<<2)
    * Jr $t0 **(reg: 32bits)**
        * PC (Target Address) ← $t0
    * bits가 클수록 더 멀리 Jump
        * Out of range인 경우 더 멀리 jump할 수 있는 Instruction을 사용
