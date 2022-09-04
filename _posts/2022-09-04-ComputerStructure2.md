---
layout: single
title: Ch 2. Instructions&#58; Language of the Computer -(1)
toc: true
toc_sticky: true
categories: Structure
published: true
---

Instructions:
<u>Computer</u> 의 언어
* Pentium(인텔에서 만든 PC용 마이크로프로세서의 상표명)
* M1 Chip
* MIPS
* ARM

이런 칩들마다 각기 다른 언어를 가짐

1. Introduction to Instruction Set Architecture

# Basics

## Machine Instruction (macro instruction)
* native language of processor
* 컴퓨터한테 특정한 operation을 하라고 얘기하는 group of bits (명령)
* Program: A **finite sequence** of instructions
* IF) C(컴파일러) -> **instruction의 집합(Memory)** -> **실행(CPU)** -> **결과저장(Memory)**

## Registers
* **CPU 안에 존재** 
* 필요한 data와 instruction을 메모리에서 가져와서 보관하는 **일시적 보관**소 (In CPU)
    * cpu는 단독으로 먼가 일을 할 수 없고 메모리에서 instruction과 data를 가져다 씀
    * instruction과 instruction을 실행하기 위한 data
* 장점: Main Memory(RAM)보다 **빠름**
    * register는 CPU안에 존재하기 때문에 access가 빠름
* 단점: **비쌈**
    * 메모리도 많이 필요하기 때문에 cpu안에 많이 집어넣진 못함 -> register로 모든 메모리 기능을 대체X
* Types of Register
    * **General** purpose register: 어떤 목적이든지 사용 가능
    * **Special** purpose register
        * **PC** (Program Counter): 다음 실행될 instruction 주소를 기록
              * instruction이 꼭 순서대로 실행X
              * EX) if문의 경우, false일 경우 다음 instruction을 뛰어넘고 그 다음 instruction을 실행
        * **AC** (Accumulator): 계산결과를 잠시 보관(축적)
              * ALU(Arithmetic Logic Unit): 사칙연산, 논리연산을 수행할 수 있는 unit(In CPU)<br/>
                      ![image](https://user-images.githubusercontent.com/63464299/188318525-00673319-a2f0-4b72-ae2d-243a0fd0ed9f.png)
        * **IR** (Instruction Register): 메모리부터 가져온(fetch) instruction을 보관
        * **Not accessible to programmers(Assembly language)**

## Instruction Set Architecture
* 프로그래머(Assembly language)가 프로세서(CPU)를 보는 **관점**
* 어플리케이션을 사용하지 않고, 프로세서와 상호작용하기 위해 필요한 정보
* **프로세서가 어떻게 디자인되고 구현되는지 디테일 필요x** (-> 4장)

* <span style="color: red">**ISA includes**</span>:
    * Processor’s **instruction set**
        * 어떠한 instruction이 있는지 
        * the set of assembly language instructions
    * Programmer **accessible register** within processor
        * 프로그래머가 사용할 수 잇는 register가 어떤 것들이 있는지
        * **Size** of each programmer-accessible registers (개수)
        * 어떤 instruction이 어떤 register을 access 할 수 있는지
    * Information necessary to interact with **memory**
        * **Memory alignment**: 메모리의 구조, 주소 체계
    * How processor reacts to interrupt from the programming view point 
        * interrupt -> I/O 

## Excercise
same Instruction Set Architecture (I3, I5, I7)
* A에서 돌아가는 프로그램은 B에서도 돌아간다
* 두 마이크로프로세서 내부의 모든 registers는 같다.
* performance와 design은 다르다


## Levels of Programming Languages

High Level Languages
* 인간에게 더 가까운 (C, Python)
* Machine **independent** (어떤 Machine이라도 관계없음 -> complier가 machine에 따라 번역)

Assembly Languages
* Machine Languge를 **기호화**시킨것 (mnemonic)
* 각각의 프로세스는 고유의 assembly language를 가짐(Machine language가 다르기 때문)
* Assembly Languages 한줄(instruction)은 machine language 한줄(instruction)과 대응
* 프로세서 안에 있는 components (register) 에 저장된 데이터를 직접 조종가능

Machine Languages: Instruction(language of machine)
* 프로세서에 Binary code(0/1)을 전달해야 특정한 operation을 수행
* native language of processor
* Machine **dependent**
* 프로세서는 논리회로로 구성


## Compiling
**Same** High-Level Language -> Run on **different processors**<br/>
Ex)
* Compiler for PC: gcc -> Pentium object code
    * Other Pentium object files + Pentium object code -> Pentium linker
    * -> Pentium Executable file(Machine Language) -> Pentium PC
* Compiler for SPARC -> SPARC object code
    * Other SPARC object files + SPARC object code -> SPARC linker
    * -> SPARC Executable file(Machine Language) -> SPARC workstation
* Compiler for microprocessor X
    * ..


## Assembling
Ex)<br/>
Assembly Language Program **for Pentium**(source code): **not same**
* Pentium Assembler -> Pentium Object code
    * Other Pentium Object files + Pentium Object code -> Pentium linker
    * -> Pentium Executable file(Machine Language) -> Pentium PC

Assembly Language Program **for SPARC**(source code)
* SPARC Assembler -> SPARC Object code
    * Other SPARC Object files + SPARC Object code -> SPARC linker
    * -> SPARC Executable file(Machine Language) -> SPARC Workstation



## Instruction Format

* Assembly Language -> (convert) -> Machine code (0/1) : Specific format
* Instruction length: 8, 16, **32(MIPS)**, **64bits**… (word size 기준)
    * **fixed size**: 요즘엔 32, 64bits으로 충분
    * **variable size**: word가 부족해서 붙여서 사용
* Typical instructions consist:
    * **Opcode**: **operation**(+, -, ×, ÷)
        * opcode: k bits, 2^k instructions(+, -,…  if) 3bits -> 8개의 operation 사용가능)
    * **Operands**: 데이터의 위치, 데이터를 표시하는 방법
        * Operand의 개수
        * operand 표시방법
        * address part: m bits, 2^m different memory locations access

