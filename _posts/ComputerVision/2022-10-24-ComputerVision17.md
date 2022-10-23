---
layout: single
title: Image Features & Matching
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Image Feature

## What is an image feature?
* **image feature(특징점)**<br/>
   * 특정한 application을 위한 계산을 수행할 때 필요한 정보
   * 영상 내에 담겨있는 정보들을 추출해서 해당 문제를 품
   * application<br/>물체 검출, 물체 추적, 두 이미지 결합(파노라마)
* specific structures
   * points, edges, objects
* 특정 픽셀의 이웃한 픽셀들의 관계를 활용하여서 생성

## What is a good feature?
* Illumination
* Translation
* Scale
* Rotation
* Perspective transform
* Computationally inexpensive
* Memory efficient

## Several Images features
extractor(detector): 영상 내에 특정한 위치가 feature인지 아닌지를 판별해주는 것
descriptor: 특정한 위치가 feature라고 판별되었을 때 그 위치에 있는 픽셀과 그 주변 픽셀들에 대한 묘사를 하는 것
* Harris Corner detector(O)
* SIFT detector(O) descriptor(O)
* MSER, SURF - SIFT 변종 detector(O) descriptor(O)
* ORB detector(O) descriptor(O)

## ORB
* oFast detector + r-BRIEF descriptor
    * FAST
        * 계산량이 적어서 빠르게 동작
        * 가운데 있는 픽셀 p가 feature인지 아닌지는 주변 픽셀들 값으로 결정
        * 임의로 원을 그림 
        * 원의 둘레에 해당하는 픽셀들 값을 확인
        * 픽셀들 중 연속적으로 픽셀 p보다 밝기값이 크거나 작다면 픽셀 p는 feature값이 됨
    * BRIEF
        * 픽셀 p가 feature로 판별이 되었을 때 이 p를 묘사하는 방법
        * 픽셀 p를 기준으로 임의의 위치를 지정해놓고 해당 위치의 픽셀값들의 대소관계를 토대로 0 혹은 1의 binary string을 생성
        * string으로 해당영역과 픽셀 p를 묘사하는 방식
    * fast 
    * illumination / rotation-invariant


# Image Matching
두 개의 영상이 유사한지 안한지 혹은 유사한다면 어떠한 위치관계를 가지고 있는지 알려주는 것
Process
1.  두 개의 영상의 feature 추출
2. 각각의 feature를 적절한 feature descriptor을 토대로 묘사
3. feature descriptor를 기반으로 두 영상에 있는 feature들이 얼마나 유사한 지 비교
4. 비교한 feature들이 얼마나 good matching에 해당하는 지 판별
what is a good matching?
* feature A와 B가 오직 이 경우에 대해서만 유사한 경우
* NNDR(Nearest neighbor distance ratio)
    * = distance to best match / distance to second best match
    * NNDR값이 작을 수록 good matching에 가깝다

## Convolutional Neural Network
* The features that were explained before are called hand-crafted features because humans invented them
* Nowadays, features using convolutional neural network(CNN) are widely used.
* Relu
    * kind of non-linear function, and it is widely used as an activation function in neural network
    * it is to increase the non-linearity in images
