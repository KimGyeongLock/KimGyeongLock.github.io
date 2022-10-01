---
layout: single
title: GrabCut
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Introduction
* Image Segmentation method
* object를 배경과 분리
* 모든 배경영역 = black
* boundary rectangle을 object에 꽉차게 그린다.

--------

# Steps
1. **User inputs the rectangle. Everything outside this rectange will be taken as sure background. Everything inside rectangle is unknown**
    * rectangle을 설정
    * 사각형 밖에 있는 모든 것들은 배경으로 인식 -> object는 사각형안에 꽉 채워야한다
    * 사각형 안에는 background도 포함되어 있기 때문에 unknown
    
2. **Computer does an initial labelling depending on the data we gave. It labels the foreground and background pixels (or it hard-labels)**
    * initial labelling 실행
    * 사각형 안의 pixel들은 initially foreground labelling
    * 사각형 밖으 pixels은 background labelling
    
3. **Now a Gaussian Mixture Model(GMM) is used to model the foreground and background**
    * GMM을 사용하여 foreground와 background를 modelling
    
4. **Depending on the data we gave, GMM learns and create new pixel distribution. That is, the unknown pixels are labelled either probable foreground or probable background.** 
    * 우리가 제공한 데이터에 따라, GMM은 새로운 픽셀 분포를 학습하고 생성
    * 알 수 없는 픽셀은 probable foreground 또는 probable background로 표시
    
5. **A graph is built from this pixel distribution. Nodes in the graphs are pixels Additional two nodes are added, Source node and Sink node. Every foreground pixel is connected to Source node and every background pixel is connected to Sink node.**
    * 픽셀 분포에 의해 그래프 작성, 픽셀: 그래프의 노드
    * Source node와 Sink node라는 두 개의 노드가 추가
    * foreground pixel - Source node
    * background pixel - Sink node
    
6. **The weights of edges connecting pixels to source node/end node are defined by the probability of a pixel being foreground/background**
    * 픽셀을 소스 노드(엔드 노드)에 연결하는 edge의 가중치는 픽셀이 foreground/background일 확률로 정함
    
7. **The weights between the pixels are defined by the edge information or pixel similarity. If there is a large difference in pixel color, the edge between them will get a low weight.**
    * 픽셀들 사이의 가중치는 edge 정보 또는 픽셀 유사성에 의해 정의
    * 픽셀 색상에 큰 차이가 있다면, pixels 사이의 edge의 가중치 = low
    
8. **A minute algorithm is used to segment the graph. It cuts the graph into two separating source node and sink node with minimum cost function. The cost function is the sum of all weights of the edges that are cut.**
    * 그래프를 분할하기 위해 mincut 알고리즘 사용
    * 최소 비용 함수(minimum cost function)를 사용하여 그래프를 Source node와 Sink node로 분리
    * 최소 비용 함수 = 절단된 edge의 모든 가중치의 합
    
9. **After the cut, all pixels connected to Source node become foreground and those connected to Sink node become background.**
    * 절단 후, Source node에 연결된 모든 픽셀 -> foregroud
    * Sink node에 연결된 픽셀 -> background
    
10. **The process is continued until the classification converges.**
    * classification(분류)가 수렴할 때까지 반복

## GMM
* **Conditional probabilities**<br/>
  ![Pasted Graphic 1](https://user-images.githubusercontent.com/63464299/193404373-1ddb794b-98ba-415e-9288-6e1e7170d8c5.png)

* **Bayes rule**<br/>
  ![Pasted Graphic 2](https://user-images.githubusercontent.com/63464299/193404378-51dd0482-8d8f-4e2f-aac8-a8e85788c8ec.png)

 * Assume A is pixel value, and B is background
     * p(A\|B)를 알아낼 수 있다면, 특정 픽셀 값이 배경일 확률을 알 수 있습니다 -> p(B\|A)
 * Background estimation using GMM
     * Determine the number of mode of GMM
     * At the training stage, estimate mean and variance of each Gaussian model with the training data
          * ->estimate p(A\|B)
          * Ex)<br/>
            Background image is totally white<br/>
            P(255\|Background) = 1<br/>
            P(0\|Background) = 0
     * Each pixel is classified into background/foreground by calculating p(B\|A)
          * P(background\|255) = high
          * P(background\|0) = low
          * P(background\|128) = half
          
---------

# GrabCut operation
* void **grabCut**(cv::InputArray img, cv::InputOutputArray mask, cv::Rect rect, cv::InputOutputArray bdgModel, cv::InputOutputArray fgdModel, int iterCount, int mode)
    * **img** - 입력영상
    * **mask** - background, foreground를 지정하는 mask image (actually output)
    * **rect** - foreground가 있는 사각형의 좌표
    * bdgModel, fgdModel - Array used internally by algorithm 
    * iterCount - Number of iterations the algorithm must run
    * mode - There are two types, GC_INIT_WITH_RECT and GC_INIT_WITH_MASK, each using a rectangle or mask to perform this algorithm
    * 4,5,6,7th parameters - 알고리즘 관련
