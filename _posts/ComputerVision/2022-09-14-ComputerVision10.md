---
layout: single
title: Drawing Function
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Rectangle
* void rectangle(Mat& img, Point pt1, Point pt2, const Scalar& color,
                <br/>int thickness = 1, int lineType = 8, int shift = 0)
    * **img**: 사각형을 그릴 영상
    * **pt1, pt2**: 사각형을 구성하는 꼭짓점 좌표(반대 대각선)
    * **color**: 사각형의 색상
    * **thickness**: 선의 두께
        * 음수 - filled rectangle
    * **lineType**: 선의 타입 (opencv documentation 참조)
    * **shift**: 보다 사각형을 정교하게 그리고 싶을 때 (중요x)


* void rectangle(Mat& img, Rect red, const Scalar& color,
                <br/>int thickness = 1, int lineType = 8, int shift = 0)
    * **Rect**: Rect(x_LT(좌상단x), y_LT(좌상단y), width, height)

----------------

# Line/Circle
* void line(Mat& img, Point pt1, Point pt2, const Scalar& color,
           <br/>int thickness = 1, int lineType = 8, int shift = 0)
    * **pt1, pt2**: 선의 양 끝 점
    * **lineType**:
        * **8**: 8-connected line (대부분)
        * 4: 4-connected line
        * CV_AA: antialiased line


* void circle(Mat& img, Point center, int radius, const Scalar& color,
              <br/>int thickness = 1, int lineType = 8, int shift = 0)
    * **center**: 원의 중점
    * **radius**: 원의 반지름

----------------

# Polygon(다각형)
* void fillPoly(Mat& img, const Point** pts, const int* npts, int ncontours,
                <br/>const Scalar& color, int lineType = 8, int shift = 0, Point offset = Point())
    * **pts**: 각각의 꼭짓점들을 포함하는 array
    * **npts**: 각각의 꼭짓점들이 개수
    * **ncontours**: 윤곽선의 개수
    * **offset**: optional offset of all points of the contours(중요x)
* 하나의 다각형만 그리는 것이 아니라 여러 개의 다각형을 동시에 그릴 수 있다

----------------

# Write text
* void putText(Mat& img, const string& text, Point org, int fontFace, double fontScale,<br/>
            Scalar color, int thickness = 1, int lineType = 8, bool bottomLeftOrigin = false)
    * **text**: text 내용
    * **org**: text의 위치(bottom-left corner- origin)
    * **fontFace**: 글체
    * **fontScale**: 글자의 크기
    * **bottomLeftOrigin**: true-bottom-left corner, false-top-left-corner

* String cv::format(const char *fmt, …)
    * 매 프레임마다 다른 텍스트를 적고 싶을 때 
    * printf랑 유사하게 text string을 리턴	
