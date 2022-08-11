---
layout: single
title: \[예습] Basics of Color
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Basics of Color

**Primary colors** of light(빛의 삼원색)
* Blue
* Green
* Red<br/>
(OpenCV순)

**Secondary colors** of light(색의 삼원색)
* Magenta(red + blue)
* Yellow(red + green)
* Cyan(green + blue)

**Achromatic color**(무채색)
* Without color 색상 정보 존재x
* The ratio of each color component is same


# Color Models

## RGB
* **R-channel**
* **G-channel**
* **B-channel**
* 각각의 채널에 대한 intensity level = 256 [0 ~ 255]
     * Red = (255, 0, 0)
     * White = (255, 255, 255) -> 무채색
     * Black = (0, 0, 0) -> 무채색

<img width="197" alt="스크린샷 2022-08-11 오후 9 30 55" src="https://user-images.githubusercontent.com/63464299/184138197-40a67f53-7842-4973-a986-ba3e2793190b.png">
> Achromatic color: Black과 White의 대각선

## HSI
* **Hue-channel**
  * the dominant wavelength in a mixture of light waves (색조)   
* **Saturation-channel**
  * the relative purity or the amount of white light mixed (선명도)
  * S가 클수록 -> clear color
* **Intensity-channel**(Brightness)
  * achromatic notion of intensity (밝기)
  * I가 클수록 -> bright color
  * HSI = HSV (Value)

<img width="265" alt="스크린샷 2022-08-11 오후 9 35 00" src="https://user-images.githubusercontent.com/63464299/184139195-463defae-1afa-40f3-8e4f-4e67ec57224d.png">
> Achromatic color: 도형의 심 
>
|Channel|Model|Range|OpenCV|
|---|---|---|---|
|Hue|원의 각도|0<H<360|0<H<180|
|Saturation|원의 중심에 가까운 정도|0<S<1|0<S<255|
|Intensity|도형의 높이|0<V<1|0<V<255|


## YCbCr
* **Y**: Brightness
* **Cb**: Difference between blue value and brightness (B-Y)
* **Cr**: Difference between red value and brightness(R-Y)

## Grayscale image(흑백 사진)
* Hue, Saturation = 0
* The lightness(or brightness) is the only parameter 
* 0(Black)-128(Gray)-255(White)
