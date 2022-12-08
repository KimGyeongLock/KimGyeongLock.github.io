---
layout: single
title: Ch 6. Storage and Other I/O Topics
toc: true
toc_sticky: true
categories: Structure
published: true
---

# Intro
## Five Components of Computer
1. **Control**
2. **Datapath**
3. **Memory**
4. **Input**
    * Keyboard
    * Mouse
5. **Output**
    * Display
    * Printer

* Disk, Network
    * 파일을 읽거나 내보내면 input device
    * 파일을 쓰거나 불러오면 output device

## Motivation for I/O Systems
* 사람과 컴퓨터가 상호작용하는 방법
* 컴퓨터에게 Long-term memory 제공
* 로봇, 드론, 무인자동차

----------

# I/O Device
* 특징
    * **Behaviour** : 무슨 일
        * input
        * output
        * storage
    * **Partner** : 누구와 작용
        * human
        * machine
    * **Data rate** : 얼마나 빠른지
        * bytes/sec
        * transfers/sec
        * partner가 사람인 device가 machine보다 더 느림
* I/O bus connections
    * processor, memory와 I/O devices를 가장 간단하게 연결해주는 System

----------

# BUS
* CPU, memory, I/O controllers 간의 interconnections 필요
* **Bus**
    * **shared communication channel**
    * Parallel set of wires for data and synchronization of data transfer
    * **병목현상** 발생 가능
* Performance 영향
    * wire length
    * number of connections
* 더 빠른 connections 대안 : networks 
    * Bus말고 다른 topology를 이용해서 더 빠르게 Communication

## Bus Types
* **Processor-Memory buses**
    * **Short**, high speed
    * 디자인은 메모리 구성과 일치
* **I/O buses**
    * **Longer**
    * multiple connections - slow
    * bridge를 통해 processor-memory bus와 연결

## Advantages of Buses
* **Versatility**
    * 쉽게 device 추가
    * 같은 bus standard를 사용하는 computer system끼리 이동 가능
* **Low Cost**
    * wires set is shared

## Disadvantage of Buses
* communication **bottleneck**
    * bus의 bandwidth은 최대 I/O throughput을 제한
* 최대 bus **속도 제한** 영향 요소
    * bus length
    * device 갯수
    * device의 차이
        * latencies
        * data transfer rates

## Bus Basics
**Bus**
* **Control Lines**
    * Signal requests
    * anknowledgments
    * data lines에 있는 정보의 type 표시
* **Data Lines**
    * Data
    * Address
    * Complex commands

**Bus Transaction**
* A sequence of Bus Operations (Request, Response)
* single request에서 시작
* Two parts
    * Sending Address
    * Receiving or Sending Data

## Synchronous vs Asynchronous Bus
* **Synchronous Bus**
    * control lines에 clock 포함
        * acknowledgment 필요 없음
    * a fixed protocol for communication that is relative to the clock
    * 장점: run very fast
    * 단점: 모든 device가 같은 clock rate, fast 한계(clock skew)
* **Asynchronous Bus**
    * not clocked
    * 다양한 장치 수용
    * clock skew 걱정없이 길게 할 수 있음
    * handshaking protocol
        * request, acknowledgment 필요<br/>
      1. ‘ReadReq’ (I/O -> Mem) : I/O sends address
      2. Mem acknowledges ‘ReadReq’ / I/O releases ‘ReadReq’, ‘data(address)’
      3. Mem drops ‘Ack’
      4. Mem sends ‘data’, ‘DataRdy’ : 데이터 준비
      5. I/O acknowledge ‘data’, ‘DataRdy’
      6. Mem releases ‘data’, ‘DataRdy’
      7. I/O drops ‘Ack’

----------

# I/O Management
* Issues
    * 사용자 I/O 요청이 장치 명령으로 변환되어 장치로 전달되는 방법
        * **Memory Mapped I/O** vs **Special I/O Instructions**
        * **Polling** vs **Interrupt**
    * 메모리에서 데이터 전송 방법
        * **DMA** (Direct Memory Access)

## Instruction Set Architecture for I/O
* **Special Input/Output Instructions**
    * (write, output, with ..)
* **Memory Mapped Input/Output** (MIPS)
    * input: load, output: store
    * address space(Not regular)에 I/O devices 할당
    * I/O devices 안에 있는 register에 대응
    * <https://kimgyeonglock.github.io/structure/ComputerStructures5/>

## I/O Device Notifying the OS
* OS가 알 필요가 있을 때
    * I/O device가 operation을 끝냈을 때
    * 에러가 발생했을 때
* **Polling**
    * I/O Device의 변화를 주기적으로 확인
    * I/O Device는 **status register**에 정보 입력
        * **Control Register** : read/write할 준비가 되었는지
            * 0=>1 : ready to read/write (Control register)
        * **Data Register** : data를 포함
            * 1=>0 : load(input) or store(output) (Data register)
    * OS는 주기적으로 status register를 확인
    * 장점: Simple, processor가 모두 control and work
    * 단점: 많은 CPU 시간 낭비 : spin-waiting => Exception mechanism
* **I/O Interrupt**
    * I/O Device에 어떤 변화가 일어나면 I/O Device가 CPU에게 알림
    * I/O device가 operation을 끝냈을 때, attention(error)이 필요할 때
	1. I/O interrupt
	2. Save PC
	3. Jump to interrupt service routine
	4. Perform transfer
    * 장점: 사용자 프로그램 진행은 실제 전송 중에만 중단됨
    * 단점: special hardware 필요
        * interrupt 발생 (I/O device)
        * interrupt 감지 (processor)
        * interrupt 이후 재개할 적절한 state 저장 (processor)
* **Exception**
    * CPU 내에서 발생
    * undefined opcode, overflow, syscall…
* **Interrupt**
    * 외부 I/O controller로부터 발생
* **Interrupt (including exception)**
    * 특별한 주의가 필요
    * control 이동: 현재 실행중인 프로그램 -> interrupt service routine
        * CPU가 효과적으로 조작하기 위해
        * 에러 발생 시 
    * 처리과정
		1. 실행중인 과정을 벗어나고 PC와 같은 CPU의 상태를 저장
		2. 특정 interrupt에 해당하는 조치 처리
		3. CPU의 상태를 재저장, 실행중인 프로그램을 복귀
    * Interrupt is like an exception
        * instruction execution과 동기화되지 않음
        * instructions 사이에 handler 호출 가능
        * Cause information은 종종 interrupting device 식별
* **Handling Exceptions**
    * **System Control Coprocessor** (CP0)에 의해 운영(MIPS)
    * 중단된 instruction의 PC 저장
        * **Exception Program Counter(EPC)** (MIPS)
    * 무슨 문제인지 저장
        * **Cause register** (MIPS)
        * 0: undefined opcode
        * 1: overflow


## DMA
* 메모리에서 많은 양의 데이터를 옮겨야 할 때 interrupt을 자주 걸게 됨 -> CPU가 자기 하던 일을 못함
* **Direct Memory Access** (DMA)
    * CPU 밖에 위치
    * CPU 개입 없이 메모리로 데이터 블록을 전송
        * 모두 전송 후에 CPU에 interrupt
    * 하드 디스크와 같은 High Bandwidth I/O 장치의 블록 전송에 적합
