---
layout: single
title: \[예습] Basics of a Digital Image/Video
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Digital Image
- made up of **pixels**
- **Pixel** (picture element)
    - 영상(image)에 대한 정보를 담고 있는 가장 작은 단위
    - 여러 개의 값 때로는 하나의 값을 가질 수 있음
    - 픽셀의 위치는 2차원 좌표로 표현
        <img width="366" alt="스크린샷 2022-09-02 오후 5 35 23" src="https://user-images.githubusercontent.com/63464299/188099483-ba64fa5d-0745-460d-9823-0e09d004236f.png">
    - 컬러영상의 경우, 빛의 3원색(RGB)으로 색상을 표현<br/>-> 하나의 픽셀이 3개의 값을 가짐 (흑백은 하나의 값)
    - alpha blending - 4가지의값

------------

# Digital Video
- made up of **images**
- 짧은 간격으로 영상을 촬영
- Normally 비디오를 구성하는 영상들 간의 간격 **33ms**<br/>
    -> 1초/33ms = 30.30303.., 대략 1초에 **30**개의 영상 존재(fps)
- **Frame rate**
    - 1초간 촬영된 images(frames)의 수(단위: **fps** Frame Per Second)
    - High frame rate일 때 더 보기가 편하고 자연스럽, 하지만 데이터의 양이 많아짐

------------

# Intensity Level
- 하나의 픽셀이 표현할 수 있는 값의 개수
    - if) L=256, 0~255까지 표현 가능
- 보통 2의 지수승으로 존재(2^k)
- 하나의 픽셀에 해당하는 intensity level은 보통 256, 2의 8승
- 크면 클수록 촬영하는 피사체를 더 정교하게 표현

------------

# Pixel Resolution (해상도)
- 하나의 영상을 구상하는데 사용되는 픽셀의 개수
- 물체의 디테일을 표현하기 위해서는 해상도가 높아야함
- |해상도|픽셀|축약|
  |:---:|:---:|:---:|
  |VGA|640X480||
  |HD|1280X720|1k|
  |FHD|1920X1080|2k|
  |QHD|2560X1440||
  |UHD|3840X2160|4k|
- 3840(width, column), 2160(height, row)
- 해상도와 PPI(Pixels Per Inch)가 영상 전체의 퀄리티를 좌우한다
    - 해상도가 같더라도 PPI가 작으면(TV vs Phone) 퀄리티가 올라간다

------------

# Total number of bits to store a digital image
M: 세로 방향 픽셀 수<br/>
N: 가로 방향 픽셀 수<br/>
k: 하나의 픽셀에 대한 데이터를 표현하기 위해 필요한 비트 수<br/>
bits = M X N X k

------------

# Assignment
Assume that you have a video that is
* Color video
* FHD pixel resolution
* 1 Hour
* 30 fps
* What is the total amount of bits?

**Solution**)
* Color video: 하나의 픽셀당 RGB 세개의 값 -> 각각의 RGB의 intensity level = 256 -> bit = 8<br/>
-> RGB => 3byte = 24bit: k
* FHD: 1920X1080 -> M: 1080, N: 1920
* 1 Hour: 30fps X 3600 = 108000

=> 1080 X 1920 X 24 X 108000 = 5,374,771,200,000 bits = 625.70GB
