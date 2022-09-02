---
layout: single
title: \[예습] Mat operator
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Color space conversion

* Color space(색공간)
    * RGB
    * HSV
    * YCbCr
* void **cvtColor**(Mat src, Mat dst, int code, int dstCn =0)
    * Mat **src**: 입력 matrix
    * Mat **dst**: 결과 matrix
    * int **code**: 변환할 Color space code
        * **CV_BGR2GRAY**: RGB -> Grayscale
        * **CV_BGR2HSV**: RGB -> HSV
        * **CV_BGR2YCrCb**: RGB -> YCbCr
        * **CV_BGR2Lab**: RGB -> Lab
    * int **dstCn**: 결과 mat의 채널 설정 if 0) src=dst (default =0)

* void **split**(Mat src, Mat* mv)
    * multi-channel을 single-channel로 분리
    * Mat* **mv**: output array

* **merge**(InputArrayOfArray mv, OutputArray dst)
    * 여러 개의 single-channel을 하나의 multi-channel로 합병

---------

# ROI
* Region of Interest(관심영역)
* 계산량 감소를 위해 범위를 축소
* ROI에서 값 변경시 original image에서도 영향
* ```Rect rect(100, 30, 250, 300)```
    * 100, 30: 좌상단 좌표
    * 250: width
    * 300: height

---------

# Addition/Subtraction operation
* void **add** (Mat src1, Mat src2, Mat dst, Mat mask=noArray(), int dtype = -1)
    * Mat **src1, src2**: operand
    * Mat **mask**: 특정한 Roi 부분에서만 더할시 사용
    * int **dtype**: 결과영상의 depth(intensity level)
        * IF dtype = -1 )<br/>
          src1 = src2 = Intensity Level
    * dst(l) = saturate(src1(l)+src2(l) if mask(l) != 0
        * **saturate** 함수: 결과가 표현할 수 있는 범위에 오도록 설정
            * IF) src1, src2: 0-255 (8-bit single channel array)
             <br/>src1(255) + src2(255) = dst(255)
             <br/>src1(0) - src2(0) = dst(0)


* void **scaleAdd**(Mat src1, double scale, Mat src2, Mat dst)
    * dst(l) = scale * src1(l) + src2(l)
* void **absdiff**(Mat src1, Mat src2, Mat dst)
    * dst(l) = saturate( &#124; src1(l)-src2(l) &#124; )
* void **subtract**(Mat src1, Mat src2, Mat dst, Mat mask=noArray(), int dtype = -1)
    * dst(l) = saturate( src1(l) - src2(l) ) if mask(l) != 0
    * absdiff과 절대값 차이

---------

# Threshold operation
* double **threshold** (Mat src, Mat dst, double thresh, double maxval, int type)
    * 입력영상의 특정한 픽셀 값이 threshold 값 이상 혹은 이하의 경우, 해당 픽셀을 특정한 값으로 변환
        * **Maxval**: IF) src(l) > thresh dst(l) = maximal,<br/>
                      IF NOT) 0<br/>
                      When type = THRESH_BINARY
        * **Type**: 
            * **THRESH_BINARY**
            * **THRESH_BINARY_INV** :  THRESH_BINARY 반대
            * **THRESH_TRUNC** : Threshold 이상의 값 -> Threshold 값
            * **THRESH_TOZERO** : Threshold 이하의 값 -> 0
            * **THRESH_TOZERO_INV** : Threshold 이상의 값 -> 0
    * 입력(src)은 grayscale 영상(one-channel)만 가능
    * grayscale 영상으로부터 binary image를 생성
        * **binary image**: 각각의 픽셀 값이 0 혹은 1(0 혹은 255) 두 가지 값만 가질 수 있는 영상

* void **adaptiveThreshold** (Mat src, Mat dst, double maxval, int adaptiveMethod, int thresholdType, int blockSize, double C)
    * **adaptiveMethod**
        * **ADAPTIVE_THRESH_MEAN_C** : 주변 픽셀의 평균으로 threshold를 결정 
        * **ADAPTIVE_THRESH_GAUSSIAN_C** : 주변 픽셀의 가중치 평균으로 threshold를 결정
    * **thresholdType**
        * **THRESH_BINARY**
        * **THRESH_BINARY_INV**
    * **blockSize**: 인접을 결정하는 파라미터 (3, 5, 7) 
    * **C** : 평균이나 가중치 평균을 구한 값에서 특정한 상수 C 값을 뺀 값이 결과값(dst)

* void **inRange**(cv::InputArray src, cv::InputArray lowerb, cv::InputArray upperb, cv::OutputArray dst)
    * **Lowerb**: lower boundary
    * **Upperb**: upper boundary
```
cvtColor(image, image, CV_BGR2YCrCb);
inRange(image, Scalar(0, 133,77), Scalar(255, 173, 127), image);
```
>  Y: 0~255, Cr: 133~173, Cb: 77~127 에 해당하는 픽셀만 255로 변환

---------

# Others

## Mat Copy
* **Shallow copy**
    * Mat data structure consists of header and data
    * the **address** is copied (포인터, 주소 공유)
    * Use '**=**' 
         * Mat m_shallow **=** m1;
* **Deep copy**
    * Use **clone()** 
    * 새로운 Matrix 생성과 copyTo() 수행 
         * Mat m_deep = m1**.clone()**;
* **copyTo** (another way of copying matrix)
    * void copyTo(OutputArray m, InputArray mask)
        * m: 복사본이 저장될 행렬.<br/>만약 *this 행렬과 크기 및 타입이 다르면 메모리를 새로 할당한 후 픽셀 값을 복사
        * mask: *this와 같은 크기의 작업 마스크.<br/> CV_8U 유형
			마스크 행렬의 원소 값이 0이 아닌 좌표에서만 행렬 원소를 복사합니다

## Mat Conversion
* Mat **convertTo**(OutputArray m, int rtype, double alpha=1, double beta=0)
    * 입력 Array의 데이터 타입을 변환 
    * **rtype**: 변환시킬 type
    * **alpha, beta**: 픽셀의 값을 변환 시켜주고 싶을 때 사용
    * m(x, y) = saturate_cast<rType> (alpha * (*this)(x,y) + beta)
         * (*this)(x,y): 원래 픽셀값
         * **saturate** 함수: 결과가 표현할 수 있는 범위에 오도록 설정
            * IF) src1, src2: 0-255 (8-bit single channel array)
             <br/>src1(255) + src2(255) = dst(255)
             <br/>src1(0) - src2(0) = dst(0)
* Mat **setTo**(InputArray value, InputArray mask=noArray()
    * 특정한 메트릭스에 대해서 각각의 메트릭스의 픽셀 값들을 value로 치환
    * **Mask**: 특정한 ROI에 대해서 수행, 설정이 없으면 default **All**
* Void **convertScaleAbs**(InputArray src, OutputArray dst, double alpha=1, double beta=0)
    * Dst(l) = saturate_cast<**uchar**> (&#124;src(l)&#124; * alpha + beta)
    * 항상 type은 unsigned character
    * convertTo와 매우 유사하나, 차이점: **&#60;uchar&#62;, &#124;src(l)&#124**
 
