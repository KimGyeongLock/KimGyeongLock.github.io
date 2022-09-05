---
layout: single
title: Spatial Filtering
toc: true
toc_sticky: true
categories: Vision
published: true
---


# Introduction
* **Spatial filtering**
    * **Spatial filter**를 활용하여 전처리를 수행
    * = spatial masks, kernels, templates, windows
    * 사전에 정의한 spatial filter를 픽셀 위에 배치
        * 보통 spatial filter의 크기는 3x3, 5x5 ,7x7 (홀수개의 픽셀로 구성)
        * 필터링을 수행하고 싶은 픽셀을 마스크의 가운데에 위치 (필터를 위치)
    * IF) 3x3 spatial filters
        * g(x, y) = w(-1, -1)f(x-1, y-1) + w(-1, 0)f(x-1, y) + …w(0,0)f(x,y) + w(1, 1)f(x+1, y+1)
        * 각각의 계수(w)와 해당하는 픽셀들의 값(f)을 곱하는 것의 합
        * f(x, y) -> g(x, y) transition

----------

# Spatial filtering
**계수(coefficient)**에 따라 다양한 결과를 생성

* **Mask size**
    * 중요한 역할
    * 작으면 작을수록 작은 잡음을 제거
    * 큰 물체들을 블러, mask크기를 증가 -> 계산량 증가 -> 상황에 맞게 마스크 크기 설정

## Averaging filter 
* = low pass filters
* 픽셀값을 필터 마스크 내부에 주변에 있는 이웃 값들의 평균으로 대치
* 장점: **random noise 제거**
* 단점: 영상자체가 흐릿(**bluring**)
* filter mask<br/>
   <img width="324" alt="스크린샷 2022-09-05 오후 11 40 42" src="https://user-images.githubusercontent.com/63464299/188484209-72e5e09f-8887-48e6-81c9-309ac14fd260.png">
   > 계수값 = 1/9<br/>
   > 1/9*픽셀값들의 합 -> 9개 픽셀값의 평균<br/>
   > 특정한 픽셀에 가중치x<br/>

   <img width="327" alt="스크린샷 2022-09-05 오후 11 41 14" src="https://user-images.githubusercontent.com/63464299/188484232-d5257156-6086-4de5-9599-7f2188b5c6f6.png">
   > 가중치O<br/>
   > 가중치 평균을 구한다<br/>

## Gaussian filter
* 가중치를 **Gaussian Function**을 활용해서 averaging filter
  * Gaussian Function<br/> 
      <img width="332" alt="스크린샷 2022-09-05 오후 11 48 03" src="https://user-images.githubusercontent.com/63464299/188484316-67c6612b-dd4b-4ce5-ab4b-a165742496db.png">  
* 가장자리로 갈수록 가중치가 낮아진다

## Sharpening
* 밝기값의 차이가 발생하는 부분들을 더 강조시킴으로써 우리가 보기에 보다 영상이 엣지있게 만듦 highlight transitions in intensity clear
* 공간 도메인(spatial)에서의 미분을 수행(spatial differentiation) 
* 값의 변화가 발생하는 부분을 더 강조시켜주는 것 

* 2차미분활용
    * 2차 미분을 활용하기 위한 마스크
      <br/><img width="646" alt="스크린샷 2022-09-06 오전 12 11 49" src="https://user-images.githubusercontent.com/63464299/188485030-eaf5387b-2512-4cbd-b72c-23099344ae57.png">
    * 입력영상에서 마스크를 활용하여 모든 픽셀에 대한 2차 미분을 구함
    * 2차 미분을 구한 영상을 원본 영상에 더함
* unsharp masking
    * Unsharp mask = Original signal - Blurred signal(둥글)
        * 값의 변화가 없는 부분 = 0, 값의 변화가 발생하는 부분 = 음수 or 양수
    * Sharpened signal = Unsharp mask + Original signal
        * 값의 변화가 발생하는 부분이 더 강조

---------------

# Other filter - Median filter
* Median value(중간값)
    * 3x3 픽셀 -> median = 5th largest
    * 5번째 큰 값을 취해서 그 값을 원래 픽셀값과 Transition
    * 랜덤한 노이즈들을 제거
        * mXm 사이즈의 미디언 필터 사용시 크기가 m^2 / 2 이하인 잡음들을 제거
        * **salt-and-pepper noise or random noise 제거**에 효과적
        * Average나 Gaussian보다 연산량이 많음, 블러링 없음
