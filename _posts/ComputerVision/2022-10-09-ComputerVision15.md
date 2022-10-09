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
* Concept
<img width="419" alt="스크린샷 2022-10-09 오후 6 44 29" src="https://user-images.githubusercontent.com/63464299/194758311-78b0375c-efdf-4c76-bb55-6fc26dc71a23.png">
    * **current frame**: f(x,y,t)
        * 특정한 시간대(ti)
    * **background**: B(x,y,t)
    * **difference**: d(x,y,t)
    * 1 or 255: 움직이는 물체 등장
    * Assumption
        * 동일한 장소, 카메라 fixed
        * 조명 상태 차이가 없어야함
* successful background subtraction
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
  1. t 번째 영상에 대해서 배경을 만들 때 t 번째 영상을 기준으로 이전 i 번째 frame까지의 평균을 구함
      <img width="206" alt="스크린샷 2022-10-09 오후 7 01 48" src="https://user-images.githubusercontent.com/63464299/194758457-3be823db-1afe-4de0-8afc-d53ce6cba8bb.png">

  3. 영상이 촬영된 최초 시점부터 특정한 n번째의 영상까지의 평균을 구함
      <img width="179" alt="스크린샷 2022-10-09 오후 7 02 19" src="https://user-images.githubusercontent.com/63464299/194758466-4b5a09a4-86a3-4c1b-906d-861ccf131ff2.png">

* **Median filter**
  * n/2 번째로 큰 frame의 픽셀값으로 각 픽셀의 값을 정함
  * B(x,y,t) = median(f(x, y, t - i))
  * B(x,y,t) = median(f(x, y, t))
  
* **GMM(Gaussian Mixtual Model)**
  * GMM tries to model your data with multiple gaussian function
  * 여러개의 가오시안 함수를 활용해서 어떠한 데이터에 특정한 값이 존재할 확률이 어떻게 되는지를 모델링
  * histogram을 normalized해서 가오시안 믹스처 모델로 모델링하면 가오시안 믹스처 모델은 특정한 값이 배경일 확률을 나타내줌
  * Determine the number of mode of GMM
      * 몇 개의 가오시안을 쓸 지 결정
  * At the training stage, estimate mean and variance of each Gaussian model with the training data-> estimate p(A|B)
      * 배경영상이 주어져 있을 때 각각의 가오시안의 평균과 표준편차를 구하는 과정을 토대로 p(A|B)를 구함
      * background 영상 일 때에 특정한 픽셀값이 존재할 확률
      * Background image is totally white
      * P(255|Background) = 1
      * P(0|Background) = 0
  * Each pixel is classified into background/foreground by calculating p(B|A)(베이지 룰)
      * 현재 영상의 각각의 픽셀의 값이 A일 때 그 픽셀이 백그라운드일 확률
          * ≥ 0.5 : background
          * ≤ 0.5 : foreground
      * P(background|255) = high
      * P(background|0) = low
      * P(background|128) = half
