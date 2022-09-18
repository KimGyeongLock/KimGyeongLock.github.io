---
layout: single
title: Color Image Processing
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Color Processing

On Color Images
* Intensity transformation
* Histogram equalization 
* Spatial filtering

* RGB 각 채널에 기술들을 적용할 수 없음
  * 각각의 채널값을 독립적으로 건드리게 되면 RGB 값의 비율이 변할 수 있는데 예상치 못한 부작용 발생<br/>
    (톤이 달라짐, 화질나빠짐) -> **intensity channel**에 대해서만 수행
* Decouple the **intensity channel** and apply 
  * Converting color space into **HSI or YUV(or YCbCr)**
  * RGB: 각 채널들이 합쳐져서 intensity 라는 값을 표현, 특정한 축이 intensity에 해당하지 않음
  * HSI, Ycbcr: 특정한 채널값이 intensity값을 의미
  * Y값 혹은 I값(Intensity Level)을 건드리는 방법으로 color processing을 수행

-------------

# Usage of HSI
* Intensity images are decoupled
    * Can change the **intensity of the image only**
* **Color Slicing**
    * Find the pixels in the range of the desired color in the **Hue**-channel(색조)
    * Set all the other pixels to 0 in the **Saturation**-channel(순도)
* **Color Conversion**
    * By accessing the **Hue**-channel, we can change the regions of color


## Pseudo Coloring
목적:<br/>
* 우리 눈은 grayscale인 경우 intensitylevel 30~50까지 구별, Color는 100k~10m (민감하게 인지가능)
* Grayscale image → Color image
* To visualize the information better
* Important to include a color scale in the images to understand what the colors illustrate
* Example of pseudo-coloring: X-Ray
    * **Intensity Slicing**
        * Each intensity is assigned a color

---------------

# White balancing
* Definition
    * Global adjustment of the intensities of the colors (조명 영향을 제거)
* Simple way of color balancing
    * 원래 입력 영상의 RGB값을 3x3 matrix와 연산하여 (255,255,255) 값으로 변환 모든 픽셀의 값을 변환
    ![image](https://user-images.githubusercontent.com/63464299/190899783-bb455caa-c514-4d76-ad62-adcc50ddd487.png)
  
## 색 확인 방법
1. Using color checker
    * 원래 흰색인 영역을 확인 방법
    * 각각의 색깔이 RGB 혹은 HSI 색공간에서 어떠한 값인지 절대값이 무엇인지 알려줌
2. Estimate white color in an image
    * Gray world assumption
        * 일반적인 상황의 사진을 찍으면 그 사진의 픽셀값들의 평균은 회색에 가깝다(128,128,128)
        * 촬영한 사진의 모든 픽셀값의 평균이 (128,128,128) 이 아니면 -> matrix를 구성해서 픽셀값 conversion
