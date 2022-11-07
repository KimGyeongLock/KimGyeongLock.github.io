---
layout: single
title: Object Detection using Deep Learning
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Deep Learning in openCV
* openCV 3.3 ver 부터 Deep Learning 사용가능
    * Deep Learning Framework 지원
        * Caffe
        * TensorFlow
        * Darknet
        * Torch/PyTorch
    * pre-trained deep learning model (C++, Python)
* 사용법
    * **YOLO** (유명한 신경망 deep learning model)
    
	1. 딥 러닝 모델 불러오기<br/>
		```
		String modelConfiguration = “yolov2.cfg”;
		String modelBinary = “yolov2.weight”;

		Net net readNetFromDarknet(nodelConfiguration, modelBinary);
		```
		
	2. 딥 러닝 모델에 적합한 blob의 형태로 입력 이미지를 처리<br/>
		```
		//Convert Mat to batch of images
		Mat inputBlob = blobFromImage(frame, 1 / 255.F, Size(416, 416), Scalar(), true, false);
		```
		
	3. blob을 딥 러닝 모델에 input함으로써 물체 검출 수행<br/>
		```
		net.setInput(inputBlob, “data”); // blob input
		Mat detectionMat = net.forward(“detection_out”); // 검출 수행
		```
		
	* GoogleNet은 영상 자체가 어떠한 영상인지를 판별, YOLO는 영상 내 존재하는 물체들을 검출

---------------

# YOLO
* the result matrix of YOLO
    * 각 행은 각 bounding box를 표현
    * 845 rows
        * 이미지를 13x13 그리드로 나누고, 각 그리드는 5개의 경계 상자를 예측
        * 13 x 13 x 5 = 845
    * 85 columns
        * 각 bounding box의 4 가지 위치값
            * center_x, center_y, width, height
        * 1 box confidence 
        * 80 class confidence
