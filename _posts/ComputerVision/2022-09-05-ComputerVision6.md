---
layout: single
title: Intensity Transformation
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Definition
* Process of mapping each intensity value of an input image into the corresponding output intensity value through mathematical expression
* 입력영상의 픽셀값들을 사전에 정의한 매핑관계를 토대로 다른 값으로 매핑하는 것

어떠한 매핑함수(그래프)를 사용했는지에 따라 결과 영상이 달라질 수 있음<br/>
**함수의 종류**
* Identity함수(기본)
* **Negative 반전함수**
* **Log함수**
* Inverse log함수
* **nth power 지수함수**
* nth root 루트함수
* 고유 함수도 설정가능, 무한함수도 가능

--------------

# Image negatives
* 이미지 반전, 색상 반전
* 입력 영상의 Intensity Level = [0, L-1] 
* Negative 영상(출력) = **(output) = L - 1 - (input)**
* 어두운 영역의 디테일이 숨겨져 있는 경우, 육안으로 확인하기에 조금 더 용이하게 만들어줌

--------------

# Log transformation
* **(output) = (constant) log(1 + (input))**
    * log(1+(input)): log0=정의x, 에러 방지
* 낮은 intensity 값의 범위가 좁은 경우 더 넓혀주는 효과
    * -> **어두운 영역에 숨어있는 디테일이나 contrast를 향상**
    * **contrast**: 각각 인접한 픽셀들과의 차이, 높으면 높을 수록 선명
* <span style="color: red">**어두운 영역의 디테일을 개선시킴과 동시에 밝은 영역의 디테일은 감소**</span>
    * 영상이 밝아진다(Brighten): 픽셀값에 특정한 상수 값 1이상의 값을 곱셈, 개념이 다르다.
* To use log function, pixel type to input should be **floating point**

--------------

# Power-Law (Gamma) transformation
* **(output) = (constant) × (input) ^ γ(감마)**
    * γ(감마): 감마에 따라 결과값이 달라짐
       * **γ=1**, 입력값과 출력값이 같음
       * **γ<=1**, 어두운 부분의 디테일이 살아남, 밝은 부분의 디테일 감소   
       * **γ>=1**, 밝은 부분의 디테일이 살아남, 어두운 부분으 디테일 감소(반대)

--------------

# Piecewise-linear transformation functions
* 임의로 함수 정의
* 특정한 영역에서 다른 기울기를 가지는 함수<br/>
   <img width="335" alt="스크린샷 2022-09-05 오후 12 18 05" src="https://user-images.githubusercontent.com/63464299/188354319-eab753b6-0c42-4e54-8ad8-8d7b30129f27.png">
   <br/>
   
   <img width="304" alt="스크린샷 2022-09-05 오후 12 18 53" src="https://user-images.githubusercontent.com/63464299/188354350-98775a1e-9518-4021-903c-dab983b69234.png">
> **binary image**: 흰색(255)과 검은색(0) 두 가지 색으로만 이루어진 이미지<br/>
> **Thresholding** 
> * Mat operator의 함수
> * 특수한 형태의 intensity transformation
> * 위 intensity transformation과 같은 기능, image segementation
> * 입력영상의 특정한 픽셀 값이 threshold 값 이상 혹은 이하의 경우, 해당 픽셀을 특정한 값으로 변환
