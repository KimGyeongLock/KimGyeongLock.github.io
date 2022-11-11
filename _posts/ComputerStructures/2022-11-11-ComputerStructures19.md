---
layout: single
title: Ch 4. The Processor - (5)
toc: true
toc_sticky: true
categories: Structure
published: true
---


# 5. An Overview of Pipelining

# Pipeline Lessons
* single task의 **latency**는 줄지 않음
    * **latency**: 어떤일을 할 때 걸리는 시간
* entire workload의 **throughput** 감소
    * **throughput**: 어떤 단위시간동안에 얼마나 많은 일이 이루어졌는가
* Multiple tasks를 동시에 작업
* **Potential speedup** = **pipe stages의 개수**
* Pipeline rate는 가장 느린 pipeline stage에 의해 제한
* Unbalanced lengths of pipe stages -> speedup을 감소
* pipeline을 채우고 빼는 시간 -> speedup을 감소
* stall for Dependencies

-------------

# Speedup
* n jobs
* each job takes T seconds
* Without pipelining
    * total execution time: **Ts = n*T**
* With pipelining
    * number of stage pipe: k
    * each stage takes: T/k seconds
    * total execution time: **Tp = (n+k-1)\*T/k**
    * Ts = k\*Tp : k배 빨라짐
* speedup: **Sp = Ts/Tp = (n*k) / (n+k-1)**
    * IF) n->♾️, Sp->k
    * Therefore **Potential speedup = Number of pipe stages = k**
    
-------------

# Basic Steps of Execution
1. **Instruction fetch step (IF)**
2. **Instruction decode/register fetch step (ID)**
3. **Execution/effective address step (EX)**
4. **Memory access (MEM)**
	* R-type이 빠지고 5번으로 감
5. **Register write-back step (WB)**
    * R-type: 계산한 결과 저장
    * LW: 가져온 값 저장

-------------

# Single Cycle, Multiple Cycle, and Pipeline
* **Sequential Execution**
    * **Single Cycle**
        * 가장 긴 instruction의 clock을 기준으로 cycle time을 정함
        * 상대적으로 짧은 instruction으로 인해 Waste 발생
    * **Multiple Cycle**
        * Single Cycle의 문제점 보안
        * instruction 한개에 여러 clock을 사용
        * Ts: 1 instruction = 800ps -> 3 Instructions = 2400ps
* **Pipelined Execution**
    * Pipeline
        * Multiple tasks를 동시에 작업 (one clock)
        * Tp: (3 + 5 - 1) * 200ps = 1400ps

-------------

# Pipelining
* 쉬운 Pipelining
    * 모든 instructions이 같은 길이
    * a few instruction formats 
    * Memory operands는 load, store 2개
* 어려운 Pipelining
    * structural hazards
    * data hazards
    * control hazards

