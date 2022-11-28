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
* Performance
    * Simplified model
        * **Execution time = (Execution Clock Cycles + stall clock cycles) × cycle time**
        * stall cycles = # of instructions × miss ratio × miss penalty
    * **Miss penalty**
        * cache안에 있는 block을 Memory에서 대응하는 block으로 대체하는 시간
        * + 이 block을 processor로 보내는 시간
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

## Three placement policies

## Replacement alg

## multi-level cache
