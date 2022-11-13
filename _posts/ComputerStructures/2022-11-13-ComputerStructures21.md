---
layout: single
title: Ch 4. The Processor - (7)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 7. Major Hurdles of Pipelining

# Major Hurdles of Pipelining : Hazard
* **Hazard**
    * 다음 clock cycle에서 다음 instruction을 실행할 수 없는 상황
      1. **Structural Hazard**<br/>
        * hardware 동시 지원불가 (instruction, data memory)
        * 한 resource를 두 instructions이 access를 하려고 함
      2. **Data Hazard**<br/>
        * 아직 pipeline에 남아있는 이전 instruction의 결과로 instruction이 결정
        * 첫번째 instruction이 끝나기전에 다음 instruction이 시작되는 문제
        * data dependency
      3. **Control Hazard**<br/>
        * instruction의 결과에 따라 제어가 다른 instruction으로 전송
        * branch하지 않을 것이라고 예측 -> wrong : **flushing** instructions

# Solutions

## Structural Hazard
* **Resource Duplication**
    * I and D memories 분리
    * Time-multiplexed or multi-port register file

## Data Hazard
* **Freezing** the pipeline
    * 이전 instruction이 끝날 때까지 stall 후에 Read
* (Internal) **Forwarding**
    * 이전 instruction에서 값이 구해지면 바로 값을 패스
    * ALU result: Execution 이후 - Stall X
    * Load, Store result: Memory Access 이후 - Stall 1
* **Compiler scheduling**
    * **nop** instruction 추가<br/>
      ```
      ADD $1, $2, $3
      NOP
      NOP
      SUB $4, $1, $5
      ```
    * **순서 재배열**<br/>
        ```
        ADD $1, $2, $3
        lw $6, 100($7)
        AND $8, $8, $10
        SUB $4, $1, $5
        ```

## Control Hazard
* **Stall**
    * branch 유무를 결정하는 Memory Access단계까지 stall 후에 다시 Instruction Fetch부터 시작
* **Optimized branch processing**
	1. branch 유무를 빨리 알아내는 법
	2. target address를 빨리 계산하는 법
    * Branch execution을 ID stage로 이동
        * branch 주소 계산 이동 (Add, Shift left2)
        * branch test 이동 (XORs and OR)
        * branch시 한 instruction만 flush하면됨
        * IF.Flush control line : IF/ID 레지스터를 지우면 가져오기 명령이 nop로 변환
* **Branch prediction**
    * Simple approach
        * always predict branch will fail
        * If the prediction is wrong -> insert a **bubble**
        * pipe안의 instruction flush & branch target address에서 instruction Fetch
    * Static Branch Prediction
        * Never branch - branch가 절대 일어나지 않을 것이라는 가정
        * Always branch - branch가 항상 일어난다는 가정
        * Predict by op-code
            * beq ~ never branch
            * bne ~ always branch
    * Dynamic Branch Prediction
       * Branch Prediction Buffer or Branch History Table
          * 최근 branch한 기록들을 memory에서 참조
       * **Simple 1-bit prediction scheme**
          <img width="535" alt="스크린샷 2022-11-13 오후 1 25 11" src="https://user-images.githubusercontent.com/63464299/201505766-abbb1c1c-95c6-4c9c-885d-11cbc6d5d183.png">
          * Prediction 2번 틀림 (entering, exiting the loop)
		   * **2-bit prediction scheme**
          <img width="614" alt="스크린샷 2022-11-13 오후 1 27 28" src="https://user-images.githubusercontent.com/63464299/201505773-72c6c071-e0a4-4e6e-892f-3b5e1365ba76.png">
          * Prediction 한번 틀림 (exiting the loop)
