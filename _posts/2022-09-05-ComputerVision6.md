---
layout: single
title: Intensity_Transformation
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Definition
* Process of mapping each intensity value of an input image into the corresponding output intensity value through mathematical expression
* 입력영상의 픽셀값들을 사전에 정의한 매핑관계를 토대로 다른 값으로 매핑하는 것

어떠한 매핑함수를 어떠한 그래프를 사용했는지에 따라 결과 영상이 달라질 수 있음
* Identity함수(기본)
* Log함수
* Inverse log함수
* Negative 반전함수
* nth power 지수함수
* nth root 루트함수
* 고유 함수도 설정가능, 무한함수도 가능

--------------

# Image negatives
* 입력 영상의 intensity level = [0, L-1], negative 영상은 (output) = L - 1 - (input)
* 이미지 반전, 색상 반전은 어두운 영역의 디테일이 숨겨져 잇는 경우 이거를 육안으로 확인하기에 조금 더 용이하게 만들어줌

--------------

# Log transformation
* (output) = (constant) log(1 + (input))
    * log0 정의x 에러 방지
* 낮은 intensity 갑들의 범위가 좁은 경우 더 넓혀주는 효과
    * -> 어두운 영역에 숨어있는 디테일이나 contrast를 향상
    * contrast: 각각 인접한 픽셀들과의 차이, 높으면 높을 수록 선명
* 어두운 영역의 디테일을 개선시킴과 동시에 밝은 영역의 디테일은 감소

영상이 그냥 밝아진다는 개념과는 다름 픽셀값에 특정한 상수 값 1이상의 값을 곱해주면 됨

--------------

# Power-Law (Gamma) transformation
* (output) = (constant)*(input) ^ γ
    * γ(감마): 정하기 나름 1이상이 될수도 있고 1이하가 될 수 있음
    * γ=1, 입력값과 출력값이 같음
    * γ<=1, 어두운 부분의 디테일이 살아남, 밝은 부분의 디테일은 감소   
    * γ>=1, 밝은 부분의 디테일이 살아남

--------------

임의로 함수 정의
# Piecewise-linear transformation functions
* 특정한 영역에서 다른 기울기를 가지는 함수
* Thresholding 특수한 형태의 intensity transformation
    * 입력영상의 특정한 픽셀 값이 threshold 값 이상 혹은 이하의 경우, 해당 픽셀을 특정한 값으로 변환
