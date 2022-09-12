---
layout: single
title: Histogram Equalization
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Introduction
* **Histogram**(도수분포도)
  * Histogram of an image with intensity levels in the range [0, L-1]
  * <img width="66" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/189585460-00b3f037-530c-4d9d-8a0f-2910edddb87b.png">
  * <img width="12" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/189585486-acde2c5e-2e1d-475a-aedf-5993dc98c81d.png">: k번째 intensity value (bin)
  * <img width="16" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/189585539-5aa1c4e0-2748-48e4-9ea8-f1dca639717a.png">: intensity value에 해당하는 픽셀의 갯수

* **Histogram normalization**
    * 히스토그램은 있는 그대로 사용하지 않고 정교화를 실행
    * **각각의 bin에 있는 값 / 영상을 구성하고 있는 픽셀의 전체 갯수** (상대도수)
      <br/>-> 각 빈에 있는 값의 범위는 0~1
    * It can be considered as a probability function(확률함수)
        * 영상 내에 특정한 값을 가진 픽셀이 존재할 확률이 정교화된 히스토그램으로 표현
* Histograms are basis for numerous spatial domain processing techniques
    * Setting the proper **number of bins** is important
        * bin의 갯수가 많은 경우, 대부분의 bin에서 유사한 값, 영상의 특성을 반영하기 어려움
        * bin의 갯수가 적은 경우, 영상의 특성을 반영하기 어려움

------------

# Histogram equalization

* **Histogram equalization**(히스토그램 평활화)
    * 일종의 전처리 방법
    * 영상의 contrast를 조절하는 방법
    * **Contrast**: 밝기 혹은 색상값의 차이, 높을수록 물체를 식별하기 쉬움(more detail)
        * 히스토그램에서 픽셀들이 상대적으로 골고루 분포
    * 항상 향상된 영상을 제공하는것x<br/>
      when a certain range of data is dominant(depending on capturing environment)

* Steps
	1. Histogram computation(계산)
	2. Find **mapping function** which distributes pixel values uniformly
	3. Apply the **mapping function** to an input image
		 * 해당함수를 활용한 intensity transformation 수행
