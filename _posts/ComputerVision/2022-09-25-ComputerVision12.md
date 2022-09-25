---
layout: single
title: Edge Detection & Line Detection
toc: true
toc_sticky: true
categories: Vision
published: true
---
# Edge Detection

## Introduction
* **Edge pixels**
    * image intensity가 갑자기 변하는 픽셀
* **Edges**
    * edge pixels의 연속된 집합
* How to detect edges? 
    * in case of 1D
        * 1차 미분의 magnitude(크기)
    * in case of **2D**
        * Image **Gradient**<br/>
	  <img width="367" alt="스크린샷 2022-09-25 오전 3 56 36" src="https://user-images.githubusercontent.com/63464299/192156760-26b4c19f-ba4d-4a27-b103-6a34407f2ebe.png"><br/>
	  > 2차원 데이터 f의 **gradient**: **x축 방향으로의 미분값**과 **y축 방향으로의 미분값**으로 구성<br/>
	  > M(x,y) : gradient의 크기<br/>
	  > a(x,y) : gradient의 각도
	  
	* Gradient Vector의 방향: 픽셀 위치에서 변화량이 가장 급격한 방향을 가리킴
	* Edge direction: gradient 방향과 90도의 수직관계
	* gradient의 방향을 활용해서 edge의 방향을 구할 수 있음 

* Effect of noise on edge detection
    * **nosie reduction** should be performed(**Blur**)


## Edge를 구하는 방법
1. **Sobel operators**<br/>
	Edge를 구하기 위해 gradient를 계산<br/>
	* gadient: x축 방향의 미분과 y축 방향의 미분으로 구성
		<img width="366" alt="스크린샷 2022-09-25 오전 4 06 37 1" src="https://user-images.githubusercontent.com/63464299/192157456-93623600-dc76-48fe-9b05-587427adc582.png"><br/>
		> x축 방향의 미분: 나의 픽셀과 x축 방향으로의 주변 픽셀과의 차이를 구하는 것
	
	* Mat pixel에 대해서 sobel 마스크를 활용을 해서 spatial filtering 실행
		* x축 미분 sobel 마스크<br/>
			<img width="111" alt="스크린샷 2022-09-25 오전 4 11 34" src="https://user-images.githubusercontent.com/63464299/192157676-9b06427e-df89-455f-b381-3ca8e5a14a65.png">
		* y축 미분 sobel 마스크<br/>
			<img width="110" alt="스크린샷 2022-09-25 오전 4 11 34 2" src="https://user-images.githubusercontent.com/63464299/192157684-58ffc443-8523-453e-bc91-e4e90c318c9a.png">
		* → 미분값 계산<br/>
			![image](https://user-images.githubusercontent.com/63464299/192157939-6b9cd881-5680-45de-a522-1fd40c9d5078.png)

2. **Canny Edge Detector**
* Algorithm
	1. **Gaussian filter**를 활용해서 영상 내 잡음 제거
	2. **Sobel edge** mask를 활용해서 gradient 크기와 각도 계산
	3. gradient 크기에 해당하는 영상에 대해서 **non maxima suppression** 수행
		* gradient 방향으로 인접한 픽셀들을 찾음
		* 선택한 픽셀의 gradient 크기가 인접한 픽셀의 gradient 크기보다 작으면 선택한 픽셀 제거
		* 주변 픽셀들 중에 최대치만 남기고 non maxima한 픽셀들은 제거
	4. **double thresholding** 수행
		* T(thresholding)H(high), TL(low) : 사용자 지정
		* M(x,y) >= TH <- edge
		* M(x,y) < TL <- non-edge
		* Otherwise <- Edge 라고 판별된 픽셀(TH보다 큰 픽셀)과 연결되어있으면 edge라고 간주

--------------

# Line Detection

## Line
* **Hough transform**
    * y=ax + b -> b = -ax + y
    * 입력영상으로 edge 영상을 받음
    * 각 edge pixel에 대해서 가능한 (a,b)에 대한 조합을 모두 구함
    * 어떠한 (a,b) 조합이 여러번 활용될 경우 그것이 영상에 존재하는 선의 방정식일 가능성이 높다.
    * 영상상의 직선이 수직방향에 가까울 경우 a는 무한대로 수렴
        * -> **𝞺𝞱** 사용 (𝞺: 원점에서 직선의 수선까지의 거리, 𝞱: row와 x축이 이루는 각도)
        * **xcos𝞱  + ysin𝞱  = 𝞺**

## Hough Transform
* Algorithm
	1. 입력으로 binary edge image가 필요 (Canny Edge Detector를 활용)
	2. 𝞺𝞱 - plane에 subdivision에 정함 ( 𝞺𝞱 값을 변화시킬 간격을 정해야함)
		* 𝞺𝞱값을 일정한 간격으로 변환시키면서 𝞺𝞱에 해당하는 직선이 선을 통과하는 지 확인
	3. Examine the counts of the accumulator cells for high pixel concentrations
	4. Examine the relationship (connectivity) between pixels in a chosen cell

* **Circle detection**
    * (x-c1)^2 + (y-c2)^2 = c3
