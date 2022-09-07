---
layout: single
title: Pixel Access
toc: true
toc_sticky: true
categories: Vision
published: true
---

# at operator
* **image.at &#60;DATA_TYPE&#62; (WANT_ROW, WANT_COL)**
    * **DATA_TYPE**: image를 구성하는 픽셀의 Data type
    * **WANT_ROW**: access 하고 싶은 y축
    * **WANT_COL**: access 하고 싶은 x축
* 장점: 안전한 방식
* 단점: 느림

```
value = image.at<uchar>(50, 100);
value_B = image.at<Vec3b>(50, 100)[0];
```
> channel = 1, data type = unsigned character, gray scale<br/>
> channel = 3, data type = Vec3b, &#91;0&#93;: blue

--------------

# pointer
* 장점: at operator보다 빠름
* **DATA_TYPE* p;**
 <br/>**p = image.ptr&#60;DATA_TYPE&#62;(WANT_ROW);**
 <br/>**p&#91;WANT_COL (* channels + BGR)&#93;;**
```
uchar* p; 
p = image.ptr<uchar>(50); 
value_B = p[100 * channels + 0]; 
```
> 포인터 선언<br/>
> 50번째 **행**의 포인터 접근<br/>
> **50번째 행**에서 **100번째 열**(100, 50), 0: blue 

--------------

# data member function
* Fast
* Hard to figure out inappropriate access
* Mat image(ROW, COL, CV_TYPE);
    * **DATA_TYPE* data = (DATA_TYPE*)image.data;**
    * **data&#91;WANT_ROW * image.cols + WANT_COL (* channels + BGR)&#93;**
        * ROW: Number of Rows(Height)
        * COL: Number of Columns(Width)
        * CV_TYPE: Type type (ex: CV_8UC3 = 8 bit 3 channels)
        * DATA_TYPE: Mat Date Type (Ex float, unsigned char)
        * WANT_ROW: The row to access
        * WANT_COL: The column to access

```
uchar* data = (uchar*)image.data; 
value_B = data[(50 * image.cols + 100) * channels + 0];
```
> **포인터는 행의 위치를 먼저 access한 후에 진행**

------------

# 질문 정리
1\. exercise 2-2<br/>
   h-1-j에서 -1을 하는 이유<br/>
   0~5 -> h=5, 좌표의 갯수때문인가??<br/>
   
=> Array, 0~h-1 -> 0, 1, 2,... h-1 -> h

2\. at<uchar>() -> 결과값: character?

=> 출력할 때 우리 눈에는 자동으로 ASCII코드로 보여진다<br/>
   하지만 컴퓨터는 알아서 픽셀값에 접근
   
3\. return 0의 의무<br/>
   int함수라서?
   
=> 상관X, 있다면 문법적으로 완성<br/>
waitKey(0)에서 key가 안눌린다면 어차피 return 0은 안먹힘<br/>

4\. image clone 필수?

=> Size를 모르기 때문에 접근을 할 수 없다. 그래서 필수!

5\. exercise4

=> avg(픽셀값) //intensity level의 평균은 픽셀값의 평균과 거의 동일 (grayscale - blakc or white)<br/>
   avg > 128 -> bright r > 1<br/>
   else case -> dark   r < 1
