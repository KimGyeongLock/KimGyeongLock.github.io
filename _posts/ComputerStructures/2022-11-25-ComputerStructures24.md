---
layout: single
title: Ch 5. Large and Fast&#58; Exploiting Memory Hierarchy - (1)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 1. Memory hierarchy general

## Large vs Fast
* Large memory = Slow
* Fast Memory = Small
* Ideal Memory = Large and Fast memory
* **Memory Hierarchy** 활용
<img width="791" alt="스크린샷 2022-11-25 오후 7 55 49" src="https://user-images.githubusercontent.com/63464299/203977532-c4fe69e1-5500-45af-bf16-e02864a85ba0.png">
> CPU와 가장 가까운 Memory: Register(In CPU)<br/>
> Level 1: Cache Memory($)<br/>
> Level 2: Main Memory<br/>
> .. ssd .. optical disk .. tape

## Principle of locality
* Locality
    * 메모리 계층 구조를 갖는 것을 좋은 생각으로 만드는 원칙
    * Temporal locality
        * 시간적
        * referenced item은 곧 다시 사용된다
        * Ex) a = b + c; d = 2*a + 1;
    * Spatial locality
        * 공간적
        * referenced item 근처에 있는 item은 곧 사용된다
        * Ex) for(i=0; i<10; i++)        sum = sum + a[i];
        * sum: temporal locality, a[i]: spatial locality
    * Processor가 access하기 좋은 곳(Cache Memory)에 locality를 배치
        * 가장 저렴한 기술로 많은 memory 사용가능
        * 가장 빠른 기술이 제공하는 speed로 access
* Modern Computer System의 Memory Hierarchy
<img width="605" alt="스크린샷 2022-11-25 오후 8 10 02" src="https://user-images.githubusercontent.com/63464299/203977547-caff3e32-d20f-460b-81e5-713102832fa5.png">

    * Smaller, faster and expensive memory가 CPU에 가까이 위치
    * 잘만 data를 갖다두면 마치 processor가 필요한 데이터는 다 On-Chip Cache에 있는데 Speed는 On-Chip Cache이지만 양은 Secondary Store(Disk)에 있는 것처럼 착각 효과
* Locality 이용
    * Memory hierarchy
    * 모든 것을 Disk에 저장
    * temporal locality or spatial locality를 Disk에서 DRAM memory로 복사
    * temporal locality or spatial locality를 DRAM에서 SRAM memory로 복사
* Memory Hierarchy의 Basic Structure
    * Upper level, Lower level
    * 주로 Cache memory에서 쓰이는 용어
        * block
            * data의 가장 작은 단위
            * 필요한 데이터만 가져오는 게 아니라 block 단위로 가져옴
        * hit, miss
            * upper level에 원하는 데이터가 있으면 hit, 없으면 miss
            * miss일 경우, upper memory에서 data를 포함한 block을 load<br/>-> CPU stalls -> 시간 소모 -> performance 감소
            * miss가 많이 발생하면 performance↓ CPI에도 영향
            * 그럼에도 불구하고 hierarchy를 쓰는 이유: Program에 locality를 포함 -> 성능은 확실히 좋아짐 (Principle of Locality)
