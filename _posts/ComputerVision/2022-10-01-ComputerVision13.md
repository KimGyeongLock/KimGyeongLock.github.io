---
layout: single
title: Image Segmentation
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Introduction
**image/video segmentation**
* 디지털 영상을 여러개의 영역으로 분할
* 응용
    * **Object classification** 
        * 눈으로는 구별할 수 없지만 밝기값 측면에서 유사한 값들을 0/255 두개의 값으로 만 표현

* Input: **gray-scale image**
* Output: **binary image**(0/255 or 0/1)
    * for two-class problems (foreground(object) and background)

-----------

# Thresholding
## Basic concepts
* Assumption
    * background와 object의 밝기값이 다름
    * 배경영역 내에서, 물체영역 내에서는 밝기값이 유사 (homogenous)
    * Images with one object and one background
        * two modals histogram
        * T: Thresholding은 modal의 사이
        * g(x,y) = 1 ( f(x,y)>T )
           <br/>   =0 (otherwise)
        * **binary image**
    * Images with one object and two backgrounds (or two objects and one background)
        * three modals histogram
        * g(x,y) = a (f(x,y) > T2)<br/>
            = b (T1 < f(x,y) <= T2)<br/>
            = c (otherwise)
        * **Not binary image**

## Challenges
* Noise(잡음)
* Illumination and reflectance
* -> Histogram이 이상하게 됨
* Thresholding after applying **smoothing(Blur)**
* -> 더 좋은 결과를 얻을 수 있다. 

## Types
* **Global thresholding**
    * **동일한** threshold를 **모든 픽셀**에 적용
* **Local (adaptive) thresholding**
    * **다른** threshold를 **각 픽셀**에 적용

-----------

# Global Thresholding
## Basic method
Assumption: 영상이 하나의 물체와 배경으로 구성
1. 임의로 하나의 Threshold T1를 정함
2. T1를 이용해서 segmentation을 수행 -> 하나의 영상이 두개의 그룹으로 분할
3. 각 그룹에 해당하는 픽셀들 값들의 평균을 구함 (m1, m2)
4. m1, m2의 평균으로 Threshold를 다시 정함 (T2=(m1+m2)/2)
5. 두 개의 Threshold가 유사하다면 종료, 차이가 크다면 step 2~4까지 Threshold = T2를 이용하여 다시 반복

## Otsu’s method
* Concept
    * 다양한 threshold를 적용해 threshold를 통해서 얻어진 **두 영역의 픽셀값의 밝기값의 차이**가 가장 큰 threshold를 찾음
    * thresholding이 잘 되었는지 판단하기 위해 **histogram**을 활용
    
1. 영상에 대해서 normalized histogram
    * Normalized: each_bin / total_pixel
    
2. threshold k값으로 thresholding을 수행 -> **between-class variance** 계산
    * 두 그룹의 밝기값이 크다면 between-class variance가 크고 밝기값이 작다면 between-class variance가 작다
    
3. between-class variance가 가장 큰  Otsu threshold k를 구함

----------

# Local(Adaptive) Thresholding
* 각각의 픽셀값에 대한 threshold를 정할 때 **주변에 있는 픽셀값**들의 분포를 토대로 threshold를 정하는 방법
* Opencv 함수
   * **ADAPTIVE_THRESH_MEAN_C**
      * 주변 픽셀들의 평균값을 토대로 threshold를 정함
      * 어떤 특정한 블럭 내에 픽셀들의 평균을 취하고 특정한 상수값을 빼서 Threshold 값으로 정함
      * T(x, y) = mean of the blocksize × blocksize neighborhood of (x, y) - C 
   * **ADAPTIVE_THRESH_GAUSSIAN_C**
      * Gaussian function을 활용해서 가중치 평균을 구한 뒤에 특정한 상수값을 뺀 값을 Threshold 값으로 정함
      * T(x, y) = a weighted sum(cross - correlation with a Gaussian window) of the blocksize × blocksize neighborhood of (x, y) - C 
* Global Thresholding시 배경 부분이 object로 판단되는 경우가 있는데 Local Thresholding은 일부 해결 가능

* 함수 외 임의로 Local thresholding을 수행가능(Custom)
    * Image partitioning
        * 조명이 다양한 영상을 임의로 영상을 분할한 다음 각 분할 된 영역별로 thresholding을 수행
        * 각 분할 된 영역별로 동일한 threshold값을 가지게 thresholding을 수행
        * 영상이 어떠한 형태로 획득 되었는지 확인하고 다양한 형태로 적용이 가능
