Edge Detection

Introduction
* Edge pixels
    * image intensity가 갑자기 변하는 픽셀
* Edges
    * edge pixels의 연속된 집합
* How to detect edges? 
    * in case of 1D
        * 1차 미분의 크기
    * in case of 2D
        * image gradient
* Effect of noise on edge detection
    * nosie reduction should be performed(Blur)


Edge를 구하는 방법
1. Sobel operators
 gradient
* x축 방향의 미분과 y축 방향의 미분으로 구성
* Mat pixel에 대해서 sobel 마스크를 활용을 해서 spatial filtering 실행


2. Canny Edge Detector
* Algorithm
    * 1. Gaussian filter를 활용해서 영상 내 잡음 제거
    * 2. Sobel edge mask를 활용해서 gradient 크기와 각도 계산
    * 3. gradient 크기에 해당하는 영상에 대해서 non maxima suppression 수행
        * gradient 방향으로 인접한 픽셀들을 찾음
        * 선택한 픽셀의 gradient 크기가 인접한 픽셀의 gradient 크기보다 작으면 선택한 픽셀 제거
        * 주변 픽셀들 중에 최대치만 남기고 non maxima한 픽셀들은 제거
    * 4. double thresholding 수행
        * M(x,y) >= T1 <- edge
        * M(x,y) < T2 <- non-edge
        * Otherwise <- Edge 라고 판별된 픽셀(T1보다 큰 픽셀)과 연결되어있으면 edge라고 간주



Line Detection

Line
* Hough transform
    * y=ax + b -> b = -ax + y
    * 입력영상으로 edge 영상을 받음
    * 각 edge pixel에 대해서 가능한 (a,b)에 대한 조합을 모두 구함
    * 어떠한 (a,b) 조합이 여러번 활용될 경우 그것이 영상에 존재하는 선의 방정식일 가능성이 높다.
    * 영상상의 직선이 수직방향에 가까울 경우 a는 무한대로 수렴
        * -> 𝞺𝞱 사용 (𝞺: 원점에서 직선의 수선까지의 거리, 𝞱: row와 x축이 이루는 각도)
        * xcos𝞱  + ysin𝞱  = 𝞺

Hough Transform
* Algorithm
	1. 입력으로 binary edge image가 필요 (Canny Edge Detector를 활용)
	2. 𝞺𝞱 - plane에 subdivision에 정함 ( 𝞺𝞱 값을 변화시킬 간격을 정해야함)
		* 𝞺𝞱값을 일정한 간격으로 변환시키면서 𝞺𝞱에 해당하는 직선이 선을 통과하는 지 확인
	3. Examine the counts of the accumulator cells for high pixel concentrations
	4. Examine the relationship (connectivity) between pixels in a chosen cell

* Circle detection
    * (x-c1)^2 + (y-c2)^2 = c3
