---
layout: single
title: Detection & Tracking
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Detection(검출)

## 컴퓨터의 물체 검출 방법
* **Training stage**
    * 많은 양의 object images와 non-object images를 수집
        * \# of non-object images > # of object images
    * object를 적절하게 잘 표현하는 **features**를 찾음
    * feature에 기반하여 물체를 구분할 수 있는 **classifier**(or threshold)를 디자인
* **Test stage**
    * 입력 영상으로 부터 **features** 추출 (training stage에서 사용한 feature와 동일) 
    * **trained classifier**를 사용해서 물체의 존재 유무를 판단

## Face Dectection
* **Feature**
    * **Harr-like feature**(openCV)
        * 영상의 특정 영역에 해당하는 픽셀들의 값을 더하고 더한 두 영역의 차로 해당영역을 표현
        * 다양한 형태, 크기, 위치로 존재
* Training
    * 생성된 많은 features 중 얼굴을 구분하는 good features를 선택
        * -> **Adaboost**(Adaptive Boosting)을 사용(openCV)
    * **Boosting**: 여러 개의 weak-learner의 집합으로 strong learner를 생성
    * **Adaptive**: 각각의 weak-lerner에 weight를 다르게 조절
* **Cascade classifier**
    * many weak learners -> strong lerner
    * 여러 개의 strong lerners로 직렬 연결
        * 각각의 strong lerner를 구성하는 weak lerner의 수는 다름
        * 영상은 첫번째 strong lerner부터 순서대로 넘어감 (판별 정확성 강화)
        * 뒤에 있는 strong lerner가 weak lerner가 많은 이유<br/>: 연산량이 많아서 앞에 두면 알고리즘의 속도가 느려짐
        * non-face regions를 쉽게 제거
* **Integral image**
    * openCV 구현이 되있는 face detection algorithm은 integral algorithm을 활용
    * 좌상단~해당하는 픽셀 위치까지 사각형을 정의하고 사각형 내부에 들어가는 값들을 전부 더함
    * 연산량이 줄음

-----------

# Tracking(추적)

## Basic concept
* ROI가 사용자의 개입이나 detection algorithm을 통해 설정
* ROI를 **histograms** 혹은 **features**로 표현
* ROI **다음 frame** 내에서 best matching patch를 찾음

## Meanshift
* 어떠한 점들의 밀도가 최대가 되는 위치로 이동시켜주는 algorithm
* iterative method
* **Histogram back-projection**
    * roi영역에 해당하는 pixel들의 밝기값은 크다.
    * 밝기값이 높은 픽셀들의 밀도가 가장 높은 곳으로 기존에 설정됐던 roi를 이동시켜주는 방식
    * EX)
    * Model image(ROI) -> Hue-Saturation histogram <br/>-> Back projection -> Target image -> Probability of each pixel being part of mode image
* initialization
    * initial detection -> object model (histogram)
* histogram back projection
    * input image (next frame) -> backprojection image -> mean-shift localization

## Camshift
* Mean shift의 변종
* 물체의 크기가 변하면 roi도 변함

## Optical Flow
* the apparent motion of brightness patterns in the image
* 밝은 물체의 움직임
* **KLT alogirthm**
    * Assumption
        * Intensity of objects are not changed over consecutive frames
        * 어떠한 물체의 밝기값은 인접한 프레임에서는 변하지 않는다.
        * Movement of pixels are similar to that of adjacent pixels
        * 어떠한 픽셀의 움직임은 인접한 픽셀의 움직임과 유사
        * I(x,y,t) = I(x+𝝙x, y+𝝙y, t+𝝙t)
    * By applying Taylor series<br/>
      <img width="530" alt="스크린샷 2022-11-01 오후 11 09 10" src="https://user-images.githubusercontent.com/63464299/199253287-3d4a842e-b63f-4bb1-b2e9-acf4374018bc.png">
    * Extract features first and track the extracted features
    * 특정한 features를 영상 내에서 추출하고 feature의 그 다음 시점의 위치를  위 식을 만족시키는 𝝙x, 𝝙y를 구함
* KLT algorithm **with pyramids**
    * **큰 움직임**에도 추적이 가능하게 설계
    * Original KLT algorithm cannot
