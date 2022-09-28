---
layout: single
title: \[예습] Ch1. Computer Abstraction and Technology
toc: true
toc_sticky: true
categories: Structure
published: true
---

# Implication of Computer (Network) Technology
**Computer revolution**	
* 3차 산업혁명
* 경제적으로 실행 불가능한 응용 프로그램 실용화<br/>
  (World Wide Web, Computers in automobiles, Robot, Cell phone,<br/>
   Human genome project, peer- to-peer computing, Cloud computing,<br/>
   Smart home/factory/farm/city, Telecommuting, IoT, Big data, AI,<br/>
   Blockchain, IT convergence etc. )

------------

# Overview of Physical Implementations 
* Integrated Circuits (**IC**s): 직접회로
* Printed Circuits (PC) boards: 인쇄 회로 기판
* Power Supplies: 전원 공급기
* Chassis (rack, card case, …): 프레임
* Connectors and Cables

------------

# Classes of Computing Applications
* **Desktop computers**
   * 개인용 컴퓨터
   * 그래픽 디스플레이, 키보드, 마우스 통합
   * 데스크탑, 노트북
* **Servers**
   * 여러 사용자들을 위해 큰 프로그램 실행
   * 네트워크를 통해서만 access
   * 메인 프레임, 미니컴퓨터, 슈퍼 컴퓨터
* **Embedded Computers**
   * 미리 정해진 응용 프로그램이나 소프트웨어를 실행
   * 다른 장치 내부에 있는 컴퓨터
   * 세탁기, 자동차, 휴대폰, 비디오게임, 프린터⋅⋅⋅

------------

# What are “Machine Structures”?
* Software: 
  * Application(ex: browser) 
  * Operating System(Windows, Unix) 
  * Compiler 
  * Assembler
* Hardware: 
  * **Processor**
  * Memory
  * I/O system 
  * **Datapath & Control(CPU)**
  * **Digital Design** 
  * Circuit Design 
  * Transistors

------------

# Below Your Program
* **Application Software**
   * 고급언어
* **System software**
   * **Compiler**: 고급언어를 기계언어로 변환
   * **Operating System**: 서비스 코드
        * 입력/출력 
        * 메모리 및 스토리지 관리
        * 스케줄링 작업 및 공유 자원
* **Hardware**
   * Processor
   * Memory
   * I/O controllers

------------

# Levels of Representation
* High Level Language Program
    * [**Compiler**]
* Assembly Language Program
    * Mneumonic: 무엇인가를 연상하여 기억하기 위해 만들어진 짧은 코드
    * Symbol 추가
        * lw $15, 0($2) ← **instruction**<br/> 
          lw $16, 4($2)<br/>
          sw $16, 0($2)<br/>
          sw $15, 4($2)<br/>
          ↑**symbol**
    * [**Assembler**]
* Machine Language Program
    * 0과 1로 이루어짐
    * [**Machine Interpretation**]
* Control Signal Specification

------------

# Instruction Set Architecture (ISA)
C + A + B; (High Level Language)<br/>
-> ISA1 push A; push B; add; pop C;<br/>
-> ISA2 load A; add B; store C;<br/>
-> ISA3 ld R1, A; ld R2, B; add R3,R1,R2;, st C,R3;<br/>

=> Instruction을 표현하는 방법은 여러가지 -> 표현방법에 따라 하드웨어를 만드는 방법도 여러가지<br/>
MIPS의 고유한 방법

------------

# Computer System Organization
* **CPU**
    * **Control** (어떤 Datapath를 가야하는지 결정)
    * **Datapath**
    * 수만개의 트랜지스터를 사용하여 구현
* **I/O**
    * **Input** (mouse, keyboard)
    * **Output** (display, printer)
* **Memory**(disk drives, DRAM, SRAM, CD)
* **SoC** (System on Chip)
    * 한 개의 칩에 완전 구동이 가능한 제품과 시스템이 들어 있는 것

------------

# Technology Trends
* 용량, 성능↑ 가격↓
* Memory Capacity (Single-Chip DRAM)
    * 무어의 법칙: 마이크로칩의 밀도가 2년에 2배씩 증가
    * 황의 법칙: 1년마다 용량이 2배씩 증가

------------

# A Safe Place For Data
* 휘발성 메인 메모리
    * 전원 종료시 명령과 데이터 손실
    * DRAM(Dynamic random access memory)
* 비휘발성 이차 메모리
    * Magnetic disk
    * Flash memory
    * Optical disk (CDROM, DVD)




