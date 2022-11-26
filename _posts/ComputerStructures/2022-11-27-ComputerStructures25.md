---
layout: single
title: Ch 5. Large and Fast&#58; Exploiting Memory Hierarchy - (2)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 2. Basics of cache

## Direct mapped cache operation
* data item이 cache안에 있는지 알아내는 방법
* block size = one word of data 로 가정
* **Direct mapped**
    * lower level에서 data item은 cache에서 정확히 한 location으로 정해져 있다.
    * **Location in the Cache = (Block address) % (Number of Cache Blocks in the Cache)**
    * **Valid bit**
        * 필요한 block인지, 의미없는 block인지 구분
    * **Tag**
        * address bits의 앞 2bits
        * cache의 데이터가 요청된 단어에 해당하는지 확인
        * Ex) 10110 -> index: 110  tag: 10 data: Memory(10110) Valid bit = Y or N
    * **Valid bit = N**(아무것도 없음) -> cache miss -> main memory에서 Load -> valid bit = Y, Tag 추가
    * **Valid bit = Y, Tag 다름** -> cache miss(다른 word) -> main memory에서 Load -> valid bit 유지, Tag와 Data replaced
    * **Valid bit = Y, Tag 같음** -> cache hit (원하는 word가 데이터에 있음)
* MIPS
    * Cache = 1024 words = **index**: **10bits**(location in the cache)
    * byte-addressable = 1 word(4 bytes): **2bits**
    * **Tag Size**: 32 - 10 -2 = **20bits**
    * **Valid bit**: **1bit**
    * cache의 총 bits = 1024 * (32 + 20 + 1) = 54,272
    * n bits: 2^n * (32 + (32 - n - 2) + 1) 


## Handling cache misses
* **Read Hits**
    * this is what we want! 
* **Read Misses**
    * 읽을려고 하는 데이터가 없을 경우
* The Basic Approach to Cache Miss
    * **Stall the CPU**
        * freezing the contents of all the registers while waiting for memory
    * **Fetch block from Memory & deliver to cache**
        * a separate controller handles the cache miss fetching the data into cache from memory
    * **Restart**
        * Once the data is present, Restart the execution
* Handling Cache Misses
    * instruction memory -> instruction cache
    * data memory -> memory cache
    * Read Miss
        * for **instruction cache** 
			1. **Send PC - 4 to memory** (data cache와 차이점)
			2. Read block from memory & CPU stalls
			3. cache entry(data, tag) 작성 & valid bit 설정
			4. instruction execution restart (instruction refetch)
        * for **data cache**
            * Step 2~3과 동일

## Write policy (only to data cache)
* **Write Hits**
    * Write through
    * Write back
* **Wirte Misses**
    * read miss와 같음
* **Write through**
    * cache와 memory의 block **둘다 update**
        * data cache가 업데이트 될 때마다 memory도 write
        * memory 접근이 많다.
        * 메모리에 있는 값과 캐시에 있는 값은 항상 일치
    * miss 발생시, 전 block은 메모리에 저장할 필요 없음
        * Faster processing
* **Write back**
    * **cache안의 block만 업데이트**
    * cache block이 replace될 때(miss) 수정된 cache block은 main memory에 저장
        * **Dirty**: Dirty bit = 1
            * 메모리에서 cache로 load되 후 cache block이 update
            * replace될 때 전 block은 memory에 저장
        * **Clean**: Dirty bit = 0
            * 메모리에서 cache로 load된 후 cache block이 update되지 않음
* 장단점
    * **W-T**
        * miss 발생시 cache와 memory의 값이 일치하기 때문에 memory에 업데이트 하지 않아도 됨
        * **write buffers**
            * lower level memory write를 기다리지 않아도 됨
      <img width="509" alt="스크린샷 2022-11-27 오전 2 54 36" src="https://user-images.githubusercontent.com/63464299/204105173-a84cb32e-1e64-46ac-9c09-d07f29a1bbf3.png">
			> Processor: cache와 write buffer로 data를 write<br/>
			> Memory controller: buffer의 내용을 memory로 write
    * **W-B**
        * cache에 쓸 때마다 메모리에 작성필요 X
        * 일반적으로 W-T 보다 performance 낮음

