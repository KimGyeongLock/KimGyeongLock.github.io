---
layout: single
title: Morphological Operation
toc: true
toc_sticky: true
categories: Vision
published: true
---


* 물체 내부에 검은색 픽셀들 (배경으로 판단되는 부분들이 존재 -> 호 처리 작업이 필요(Morphological operation)
* 조각난 영역들을 병합
* Assumption
    * input: Binary image

----------

# Erosion and Dilation
* **Erosion(침식)**
    * ⊖
    * Erosion of A by B
        * B물체를 계속 이동시키면서 B물체가 A물체에 **완전하게 포함**이되는 영역만을 찾는 것
    * binary image안의 물체를 **축소**시키거나 **얇게** 만드는 효과
    * 교집합
* **Dilation(팽창)**
    * ⊕
    * Dilation of A by B
        * B물체의 **일부분이라도** A물체에 포함이 되는 영역을 찾는 것
    * 물체의 **크기를 키우거나** **두껍게** 만드는 효과
    * 합칩합
    
--------

# Opening and Closing
* **Opening**
    * **Erosion -> Dilation**
    * Smoothens contours 
         * 전체적으로 물체의 윤곽선을 부드럽게
    * break narrow isthmuses 
         * binary object의 두께가 얇은 부분들이 쪼개짐
    * eliminate small island 
         * 조그마한 점들이 제거
    * sharp peak
    * 원래 분리되어야 되는 물체가 붙어서 검출이 되는 경우 잘라내기 위해서 사용, 조그마한 잡티 제거
* **Closing**
    * **Dilation -> Erosion**
    * Smoothens contours
    * fuses narrow breaks and long thin gulfs 
         * 얇게 존재하는 영역들이 더 두꺼워지면서 붙는 경우
    * eliminates small holes 
         * 조그마한 구멍 제거
    * 원래 하나의 물첸데 간당간당하게 연결되어 있는 물체를 보완, 구멍이 너무 나 있는 경우
