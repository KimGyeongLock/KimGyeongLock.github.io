---
layout: single
title: Ch 4. The Processor - (8)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 8. Performance - From chapter1

# Performance
* Latency(Execution Time)
  * 어떤 일을 하는데 필요한 시간
    * How long does it take for my job to run?
    * 고객 입장에서 중요시 여기는 것
  * Throughput
    * 하루 동안 얼마나 일을 했는가
    * How many jobs can the machine run at once?
    * 회사 입장에서 중요시 여기는 것

-----------

# Execution Time(Latency)
* Elapsed Time
  * counts everything
* CPU Time
  * I/O, 다른 프로그램이 돌아가는 시간은 제외
  * Just 유저가 cpu에서 보내는 시간에만 Focus
* Performance = 1 / Execution Time

-----------

# CPU Time
* Clock period
    * duration of a clock cycle = clock cycle time
    * 250ps = 250 x 10^-12s
* Clock frequency(rate)
    * cycles per second = 1 / clock cycle time
    * frequency가 높을수록 Clock period는 짧아짐
    * 4.0GHz = 4000MHz = 4.0 x 10^9Hz
    
<img width="701" alt="스크린샷 2022-11-16 오전 12 10 27" src="https://user-images.githubusercontent.com/63464299/201955992-999406ca-d3fd-4bfc-98eb-a3aa671b0675.png">
    * 성능 향상
        * clock cycles의 개수 감소
        * clock rate 증가
        * 둘 다 동시에 하는 것은 쉽지 않음 -> critical path가 짧아질수록 할 수 있는 일이 한계가 잇음 -> clock cycle이 늘어남

## Proportional to Instruction Count
* Seconds / Program ∝ Machine Instructions / Program
    * instructions의 갯수가 많아지면 시간이 오래 걸림 
    * architect가 instructions 개수에 영향을 미치는 방법: 
        * Create new instructions : instruction set architect
        * instruction set을 어떻게 만드는 냐에 따라 프로그램을 실행하기 위한 instruction의 구성이 바뀜
    * Compiler writer, Application developer가 instruction count에 영향을 줌
    * Dynamic count
## Proportional to Clock Period
* Seconds / Program ∝ Seconds / One Clock Period
    * 각 cycle의 period가 짧아짐으로써 execution time이 짧아짐
    * clock period를 줄이는 방법: critical path를 줄인다!
    * clock period를 계속해서 줄일 수 있나? -> Clock to Q, setup time으로 인해 X
## Performance Equation
<img width="765" alt="스크린샷 2022-11-16 오전 12 12 57" src="https://user-images.githubusercontent.com/63464299/201956073-ac40261b-9f6c-47d5-a0af-f111e8684e57.png">
* Seconds / Program = (Instructions / Program) × (Cycles / Instruction) × (Seconds / Cycle)
    * only 3가지 terms가 필요
        * 한 두개만 좋다고 CPU Time이 빨라지는 것X 세 개 다 좋아야 한다
    * Cycles / Instruction
        * CPI: The Average Number of Clock Cycles Per Instruction For the Program
        * 프로그램마다 각각 다른 CPI를 가지는 요인
            * Cache behavior이 다름
            * Instruction mix가 다름
            * Branch prediction이 다름

-----------

# CPI(Cycles Per Instruction)
<img width="790" alt="스크린샷 2022-11-16 오전 12 11 30" src="https://user-images.githubusercontent.com/63464299/201956135-c7089ab7-8fde-4f70-8d04-6cd1cef76db5.png">
    * Instruction Count 
        * program, ISA, compiler에 의해 결정
* Weighted average CPI
  <img width="789" alt="스크린샷 2022-11-16 오전 12 03 26" src="https://user-images.githubusercontent.com/63464299/201956168-0606ac97-4a02-4e55-a27b-f3d31dfe1fb3.png">

-----------

# Other metrics
* MIPS (Million Instructions Per Second)
* MFLOPS
    * Floating Point Operations / Execution Time
* Benchmark program
* 성능이 좋을 것이라고 짐작은 가능하지만 정확하게 확신하지 못하는 척도
