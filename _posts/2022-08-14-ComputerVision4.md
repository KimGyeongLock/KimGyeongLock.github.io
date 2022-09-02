---
layout: single
title: \[예습] Basics of openCV
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Mat 
* openCV의 기본데이터 타입 
* “Matrix”
* Declaration
    * Mat (int rows, int cols, int **type**)
        * Mat mtx(3, 3, CV_32F): 3x3 floating-point matrix
        * Mat img(**1080, 1920**, CV 8UC3): 3-channel (color) image of 1920 columns and 1080 rows
    * Mat (Size size, int type)
        * Mat img(**Size(1920, 1080)**, CV 8UC3)
    * Mat (const Mat & m) 
    	* copy matrix
    * Mat (Size size, int type, const Scalar& s)
    	* Scalar: 픽셀의 특정한 값
        * Mat img(h, w, CV_8UC1, Scalar(255))  
        * multi-channel image: Scalar(255,0,0) **(B,G,R)**

## Pixel **type**
* **CV_8U: 8-bit unsigned integer: uchar ( 0~255 )**
* CV_8S: 8-bit signed integer: schar ( -128~127 )
* CV_16U: 16-bit unsigned integer: ushort ( 0~65535 )
* CV_16S: 16-bit signed integer: short ( -32768~32767 )
* CV_32S: 32-bit signed integer: int ( -2147483648~2147483647 )
* CV_32F: 32-bit floating-point number: float ( -FLT_MAX~FLT_MAX, INF, NAN )
* CV_64F: 64-bit floating-point number: double ( -DBL_MAX~DBL_MAX, INF, NAN )
* Multi-channel array: **CV_8UC3**(Color Image: 3-Channel), CV_8U(3), CV_64FC4, CV64FC(4)

**CV**: **C**omputer **V**ision

------------

# Read an image in openCV
* Display an image<br/>
  Mat **imread**(const string& filename, int flags=1)
    * Flag 1: Color image (Default)
    * Flag 2 or 0: Gray scale image
    
```
int main() {
	Mat img;
	img = imread(“lena.png”, 1);
	imshow(“Window”, img);
	waitKey(0);
}
```

------------

# Read a video in openCV

* Read a video from a **file**
    * 클래스 선언<br/>
      ```VideoCapture cap;```
        * openCV에서 제공되는 class
    * 파일 읽어오기<br/>
      ```
      if (cap.open(“background.mp4”) == 0) {
          cost << “no such file!” << endl;
          waitKey(0);
      }
      ```
      * 파일이 존재하지 않을 경우 프로그램 정지
    * 무한 루프<br/>
      ```
      while(1) {
          cap >> frame
          if(frame.empty()) {
            count << “end of video” << endl;
            break;
          }
          imshow(“video”, frame);
          waitKey(33);
      }
      ```
      * 영상의 한 frame씩 frame변수로 이동 (첫번째 frame부터)
      * 영상이 끝날때까지 출력
      * **waitKey**: 사용자의 키를 기다림(frame Interval) 영상간의 간격
          * 0 = Forever
	  * 공식: **1000/fps**
	  	* 1초 = 1000ms
		* 2배 faster -> 1000/2fps = 500/fps
	  	
	  * **milliseconds**(단위)
	  * speed를 increase or decrease
* Read a video from a **webcam**
    * ```VideoCapture cap(0);```
        * webcam device number = 0
    * ```waitKey(16);```
        * waitKey(1000 / fps);


## VideoCapture Class
* Method **GET**<br>
  비디오에 대한 상세한 정보를 확인
    * CAP_PROP_POS_MSEC: 현재 비디오 파일의 재생 위치
    * CAP_PROP_POS_FRAMES: 현재 영상의 프레임 순서
    * CAP_PROP_FRAME_WIDTH: 프레임의 가로
    * CAP_PROP_FRAME_HEIGHT: 프레임의 세로
    * CAP_PROP_FRAME_COUNT: 프레임의 총 개수
    * CAP_PROP_FPS: Frame rate(초당 존재하는 영상의 수)
    * …

