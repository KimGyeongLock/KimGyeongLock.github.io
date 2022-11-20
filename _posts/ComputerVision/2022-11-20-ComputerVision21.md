---
layout: single
title: Understanding of a Camera
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Image Sensing and Acquisition
* Image formation model
    * Illumination(energy) source
    * Scene element
    * Imaging system
        * 반사된 energy in -> Voltage waveform out
        * Sampling and quantization
            * using Intensity level
    * Output (digitized) image
* Bayer pattern
    * 초록색이 2개인 이유
        * 사람은 초록색 빛에 더 민감

-------------

# Camera Model
* 카메라: 3차원 데이터를 2차원으로 변환시켜주는 장치
* 영상 처리 분야에서는 Pinhole camera model을 사용
    * 구멍을 통해 상하좌우 반전
* Coordinate
    * World coordinate(3D)
        * 주어져 있는 3차원공간을 표현하는 좌표
        * 어떠한 물체의 위치를 표현하기 위한 좌표계 
        * 임의로 특정한 위치를 원점으로 둘수 있음
    * Camera coordinate(3D)
        * 카메라가 좌표계의 원점에 있는 상태
    * Pixel coordinate(=image plane, 2D)
        * 3차원 데이터가 카메라를 통해 매핑된 값들의 좌표
    * Normalized image plane
        * focal length가 1인 image plain(평면)을 생각하고 그 이미지 평면 내에서의 좌표값
        * Focal length: 카메라 센터와 image plane간의 거리
    * Inhomogeneous coordinates
        * 일반적으로 사용
        * 2D point -> (x,y)
        * 3D point -> (x,y,z)
    * Homogeneous coordinates
        * 영상처리 및 컴퓨터 비전 분야에서 많이 사용
        * 2D point -> (x,y,1)
        * 3D point -> (x,y,z,1)
        * (x,y,z,1) = (2x, 2y, 2z, 2) = (kx, ky, kz, k) <- equal up to scale
        * 특별한 기호 없이 무한대의 점을 표현 가능
        * Point a infinity(2D) = (x,y,0) (if x,y≠0)
* Camera projection matrix
    * 카메라 center가 world coordinate 상의 원점에 있을 경우
        * P = K[I\|0]
        * K: Camera calibration matrix 3x3
          <img width="96" alt="스크린샷 2022-11-20 오후 3 23 12" src="https://user-images.githubusercontent.com/63464299/202889397-e2244e58-116a-45ce-9c6c-6416fc599084.png">
            > f: focal length<br/>
            > sxx: x축방향으로의 픽셀크기<br/>
            > syy: y축방향으로의 픽셀크기<br/>
            > sxy: skew parameter<br/>
            > u0, v0: principal pointer의 좌표
    * rotation(~(tilde)R)과 translation(~C)가 있는 경우
        * P = K[~R\|t]
        * t = - ~R~C

