---
layout: single
title: Background Subtraction
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Video Segmentation
* 주어진 frame을 여러 개의 영역으로 분할
* Application
    * Chroma-keying(크로마키)
    * Surveillance camera(감시 카메라)

-----------

# Background Subtraction
* type of video segmentation
* foreground object 검출
  * **Current Frame - background > 특정한 Threshold**
* object가 관심 대상, 배경x
* Concept<br/>
<img width="419" alt="스크린샷 2022-10-09 오후 6 44 29" src="https://user-images.githubusercontent.com/63464299/194758311-78b0375c-efdf-4c76-bb55-6fc26dc71a23.png">
    * **current frame**: f(x,y,t)
        * 특정한 시간대(ti)
    * **background**: B(x,y,t)
    * **difference**: d(x,y,t)
    * 1 or 255: 움직이는 물체 등장
    * Assumption
        * **동일한 장소, 카메라 fixed**
        * **조명 상태 차이가 없어야함**
* **successful background subtraction**
    * 급격하거나 점진적인 조명 변화 극복
    * 반복적인 움직임
        * 나뭇잎, 파도
    * 장기간 배경 변화
        * 두고간 가방, 주차된 차
        * 배경으로 처리해야하는지
        
## Background estimation
* **Mean filter**
  * 백그라운드를 만들 때 이전 n개의 frames의 평균으로 만듦
    * n이 클수록 배경이 더 들어남
  * t번째 영상에 대해서 배경을 만들 때
      1.  t번째 영상을 기준으로 이전 i번째 frame까지의 평균<br/>
         <img width="206" alt="스크린샷 2022-10-09 오후 7 01 48" src="https://user-images.githubusercontent.com/63464299/194758457-3be823db-1afe-4de0-8afc-d53ce6cba8bb.png">
      2. 영상이 촬영된 최초 시점부터 특정한 n번째의 영상까지의 평균<br/>
         <img width="179" alt="스크린샷 2022-10-09 오후 7 02 19" src="https://user-images.githubusercontent.com/63464299/194758466-4b5a09a4-86a3-4c1b-906d-861ccf131ff2.png">

* **Median filter**
  * n/2 번째로 큰 frame의 픽셀값으로 각 픽셀의 값을 정함
  * B(x,y,t) = median(f(x, y, t - i))
  * B(x,y,t) = median(f(x, y, t))
  
* **GMM(Gaussian Mixtual Model)**
  * 여러개의 Gaussian function를 활용해서 어떠한 데이터에 특정한 값이 존재할 확률을 모델링
  * histogram -> normalized -> GMM Modeling -> 특정한 값이 배경일 확률을 보여줌
  1. Gaussian function의 개수 결정
  2. 배경영상이 주어져 있을 때, 각각의 Gaussian의 평균과 표준편차를 구하는 과정을 토대로 p(A|B)를 구함
      * p(A|B): background 영상일 때에 특정한 픽셀값이 존재할 확률
      * Background image is totally white
      * P(255|Background) = 1
      * P(0|Background) = 0
  3. p(B|A)를 계산해서 각각으 픽셀을 background와 foreground로 구분(베이지 룰)
      * p(B|A): 현재 영상의 각각의 픽셀의 값이 A일 때 그 픽셀이 background일 확률
          * ≥ 0.5 : background
          * ≤ 0.5 : foreground
      * P(background|255) = high
      * P(background|0) = low
      * P(background|128) = half
