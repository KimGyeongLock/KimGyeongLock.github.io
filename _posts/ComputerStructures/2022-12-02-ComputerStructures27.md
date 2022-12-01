---
layout: single
title: Ch 5. Large and Fast&#58; Exploiting Memory Hierarchy - (4)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 4. Virtual memory

## Virtual memory general
* Virtual Memory
    * 2 storage levels
        * primary (DRAM)
        * secondary (Hard Disk)
    * OS: memory 공유, program 보호
        * multiple processes은 메모리를 공유
        * 한 메모리를 다른 program이 access하는 문제 방지(중요)
    * 각 program이 개인의 memory를 독점한다고 착각 => multi-processing system
        * Complier, linker, loader simplified
    * virtual address
        * process의 address space 내부에 memory 전달
    * physical address
        * physical memory location 접근
    * physical memory 보다 더 많은 메모리를 사용가능
        * address space of each job > physical memory 
        * total memory of all jobs >> physical memory 
    * 일부는 main memory, 잘 사용하지 않는 것은 하드디스크에 저장 (cache처럼 활용)

## Page table
* Address Translation
    * Program은 virtual addresses 사용
        * Relocation: 프로그램은 다시 컴파일하거나 다시 연결하지 않고도 physical memory의 어느 곳이든 load 가능
    * Hardware는 virtual 제공 => physical mapping
        * translation table 필요
    * virtual address가 main memory에 없는경우 OS가 miss 처리
        * page fault -> missing data를 읽음 -> translation 생성 -> instruction 재실행
* Pages: Virtual Memory Blocks
    * virtual address -> physical address Mapping (Translation)
        * virtual address = virtual page number + page offset
        * physical address = physical page number + page offset
* Page Faults
    * Virtual memory miss
    * 데이터가 메모리에 없는 경우, disk에서 가져옴
    * page fault를 줄이기 위해 -> LRU 사용
    * writeback 사용, write-through 비쌈
* Page Tables
    * full table that index memory
    * main-memory안에 포함
    * 각 program은 각 page table을 가지고 있음
    * page table register
        * page table 시작을 point
  <img width="633" alt="스크린샷 2022-12-01 오전 9 51 46" src="https://user-images.githubusercontent.com/63464299/205115320-32580b8d-9620-4c3a-ab5a-c922994a51a3.png">

## TLB
* TLB(Translation Lookaside Buffer)
    * a special cache for address translations
    * page table의 일부를 포함
    * performance 향상: locality of reference to page table
    * TLB Hit이고 Cache에 있으면 Cache -> CPU
    * TLB Hit이고 Cache에 없으면 Main Memory -> Cache -> Main Memory
    * TLB Miss이면 Exception: 다시 page table을 TLB로 가져오는 작업
    * fully associative



