---
layout: single
title: 2D Projective Transformation
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Introduction
* **Similarity transformation**
    * rotation, translation, scaling etc
    * 물체의 형태는 변하지 않음
* **Affine transformation**
    * 형태가 미세하게 변함
    * 비율이 달라지거나 일부 찌그러짐
    * general transformation
    * 평행한 선은 여전히 평행
* **Projective transformation**
    * 측면에서 본것처럼 혹은 위에서 본 것처럼 변환
    * 원래 평행했던 선들도 평행관계를 잃어버림
    * 선은 직선으로 보존
    * = **Perspective transformation** = **Homography**

-------------

# Perspective Transformation
* 적용방법
    * 두 영상의 관계를 설명하는 행렬이 계산되어져야함
    * **3X3** dimension of matrix -> 8개의 elements를 알 필요 (8개의 식)<br/>-> 적어도 4개의 대응쌍이 필요
    * 입력영상만 있고 결과 영상이 없는 경우: 임의로 지정
