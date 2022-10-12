---
layout: single
title: \[예습] 반응형 웹 개발
toc: true
toc_sticky: true
categories: Practical
published: true
---

**Responsive(반응형)**
* 다양한 디바이스에서 보기 좋은 페이지 만들기(Phone, Tablet, Desktop)
* HTML과 CSS 사용 (JS 불필요)
* 웹 페이지를 디바이스 화면 크기에 맞춰 적합한 정보만을 표시할 수 있도록 스타일 설정
* resize, hide, shrink, enlarge, move

----------

# Setting The Viewport
* **Viewport**: 디바이스의 화면에서 보여지는 영역 (스크린 크기)
* 디바이스 마다 다른 viewport를 제어할 수 있는 방법: \<head\> 내 **\<meta\>** 태그 사용
    * **width=device-width**: 현재 페이지의 너비를 디바이스 화면 크기에 맞춤
    * **initial-scale=1.0**: 브라우저가 페이지를 로딩했을 때 처음 화면 비율

----------

# Grid-View
* **grid-view**
    * 웹 페이지를 디자인할 때 페이지 요소들을 배치하기 위해 활용하는 가상의 구분선
* **box-sizing** 속성
    * box-sizing: border-box;
    * 이 속성이 없으면 영역 크기(width or height)에 padding
    * border는 별도로 적용
* **relative positioning**
    * .menu { width: 25% }
    * .main { width: 75% }

----------

# Media Queries 
* **@**???rule
    * 특정한 규칙으로 스타일을 정하는 방식
    * @import, @font-face, **@media**, @key-frames, @charset
* **Media query**
    * 특정 조건이 만족되는 경우에 적용되는 @media rule을 사용하여 스타일을 정의하는 방식
      ```
      @media not|only mediatype and (expressions) {
        CSS-Code;
      }
      ```
    * Ex)
      ```
      @media only screen and (max-width: 768px) {
        [class*=“col-“]
          width: 100%
      }
      ```
* **Media Features**
    * max-width, max-height: 디바이스 화면(브라우저)의 너비, 높이 최대치
    * min-width, min-height: 디바이스 화면(브라우저)의 너비, 높이 최소치
    * max-color, max-color-index: 디바이스의 표현 가능한 최대 컬러 비트 수, 최대 컬러 갯수
    * orientation: 화면(viewport) 표시 방향 (landscape or portrait)
    * max-aspect-ratio, min-aspect-ratio: 화면의 가로:세로 비율 최대치, 최소치
    * resolution: 출력 디바이스의 해상도(dpi, dpcm)

----------

# Images
* **Image resizing** 
    * 화면에 표시되는 이미지의 크기를 화면 크기에 따라 조정되도록 설정
      ```
      img {
        max-width: 100%;
        height: auto;
      }
      ```
* Background Images
  ```
  background-size: 100% 100%;
  background-size: cover;
  ```
* Different Images for Different Devices
  ```
  @media only screen and (min-width: 400px) {
    body {
      background-image:url(‘img_flowers.jpg’);
    }
  }
  ```
