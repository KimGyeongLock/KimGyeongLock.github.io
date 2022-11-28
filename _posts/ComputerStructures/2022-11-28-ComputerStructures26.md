---
layout: single
title: Ch 5. Large and Fast&#58; Exploiting Memory Hierarchy - (3)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 3. Improving cache performance

## Block Size
* **Direct Mapped Cache** (MIPS)
    * **Temporal Locality(O)**
        * 메모리에서 가져오지 않고 내가 원하는 데이터를 cache에서 Fetch
    * **Spatial Locality(X)**
        * 메모리에서 데이터를 가져올 때 1 word만 가져올 수 있기 때문에 다음 word는 Fetch 불가
* **Multiple Word Direct Mapped Cache**
    * 32bits
        * Byte Offset: 2bits
        * **Block Offset: 2bits**
            * 4 words 중 내가 원하는 word가 무엇인지 찾아주는 bit
            * 00, 01, 10, 11
        * **Index: 12bits**
            * 64KB cache  = 2^16B = 2^14 word
            * 14bits - 2bits(block offset) = 12bits
        * **Tag: 16bits**
            * 32 - 14 - 2 = 16
    * **Spatial Locality(O)**
        * 한 block 안에 여러 words를 포함
        * 같은 block안에 있는 각 words는 Tag & Valid를 공유
    * Miss 발생시 block 전체를 가져옴(4 words) 
        * 시간이 오래걸림
        * **miss penalty 증가**
    * Hit Ratio 상승 -> 성능 증가
* **Performance**
    * Simplified model
        * **Execution time = (Execution Clock Cycles + stall clock cycles) × cycle time**
        * stall cycles = # of instructions × miss ratio × miss penalty
    * **Miss penalty**
        * cache안에 있는 block을 Memory에서 대응하는 block으로 대체하는 시간
        * \+ block을 processor로 보내는 시간
    * **Hit time << Miss Penalty**
    * Performance 향상 방법
        * **miss ratio** 줄이기
        * **miss penalty** 줄이기
    * **Block Size**를 증가하는 것은 Miss Ratio를 감소하는 경향
        * But, block size가 cache size의 상당 수의 비율을 차지하게 되면 miss ratio는 증가
        * Why<br/>
          1. block의 개수가 작아진다
          2. words 끼리의 Spatial locality가 줄어든다
          3. data를 전달하는 시간 증가로 비용이 증가한다

## Interleaving
* **Bank**
    * 여러 words를 쉽게 읽기 위함
    * Ex) 1 cycle: sending address<br/>
         15 cycles: reading one word data<br/>
         1 cycle: sending one word data
	1. **One-word-wide memory organization**
        * Bus: 32bits
        * 1cycle(CPU->Cache) + 4words x 15cycles(Memory->Cache) + 4words x 1cycle(Cache->CPU) = 65
	2. **Wide memory organization**
        * CPU와 메모리 사이의 메모리와 버스 확장 -> bandwidth 증가
        * 4 words를 한꺼번에 이동
        * Bus: 128bits
        * 1cycle(CPU->Cache) + 15cylces(Memory->Cache) + 1cycle(Cache->CPU) = 17
        * 비용이 많이 필요
	3. **Interleaved memory organization**
        * 메모리 확장 -> bandwidth 증가
        * 메모리를 4개의 bank로 분리, 각 메모리가 데이터를 준비해서 전송
        * 1cycle(CPU->Cache) + 15cycles(Memory->Cache) + 4words x 1cycle(Cache->CPU) = 20

## Three placement policies
* **Direct mapped**
    * 자리가 정해져 있음
    * Ex) 11100 = 100, 10100 = 100
    * Tag 일치 & Valid bit = Y  => Hit (block안에 원하는 데이터가 존재)<br/>
      -> Block offset을 사용해서 Mux를 통해 원하는 데이터 추출
* **Fully associative**
    * 빈 곳이 있으면 아무데나 들어갈 수 있음
    * **Cache Index 무시**: 위치 상관 없음, Tag 확장
    * 어느 위치든 block이 위치 가능
    * 찾으려는 데이터의 Tag와 Cache의 Tag 모두를 비교(Parallel) => **Associative Memory** 사용(비쌈)
    * Byte offset: 2bits
    * Block offset: 2bits
    * Cache Tag: 28bits
* **Set associative**
    * Set을 나누어 정해진 Set안에서 아무데나 들어갈 수 있음
    * **1-way set associative = Direct mapped**
        * 메모리 block의 위치 = block의 갯수 % cache blocks의 갯수
    * **2-way set associative: 1set = 2blocks (4 sets)**
        * 메모리 block의 위치 = block의 갯수 % cache set의 갯수
        * Ex) 12 % 4 = 0
    * **4-way set associative: 1set = 4 blocks (2 sets)**
        * Ex) 12 % 2 = 0
        * Byte offset: 2bits
        * Block offset: 2bits
        * set number: 6bits
        * Cache Tag: 22bits
    * **8-way set associative = Fully associative**
* Degree of Associativity 증가
    * 장점: miss ratio 감소 - hit ratio 증가
    * 단점: hit time 증가 (hardware complexity)

## Replacement alg

## multi-level cache
