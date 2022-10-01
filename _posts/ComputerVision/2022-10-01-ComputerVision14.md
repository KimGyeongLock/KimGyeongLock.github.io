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
1. User inputs the rectangle. Everything outside this rectange will be taken as sure background. Everything inside rectangle is unknown
    * rectangle을 설정, 사각형 밖에 있는 모든 것들은 배경으로 인식, 그래서 object는 사각형안에 꽉 채워야한다 사각형 안에는 백그라운도 포함되어 있기 때문에 unknown
    
2. Computer does an initial labelling depending on the data we gave.It labels the foreground and background pixels (or it hard-labels)
    * 우리가 준 data에 따라 initial labelling 실행, foreground와 background 픽셀에 labelling
    
3. Now a Gaussian Mixture Model(GMM) is used to model the foreground and background
    * GMM
        * Conditional probabilities<br/>
          ![Pasted Graphic 1](https://user-images.githubusercontent.com/63464299/193404373-1ddb794b-98ba-415e-9288-6e1e7170d8c5.png)

        * Bayes rule<br/>
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
4. Depending on the data we gave, GMM learns and create new pixel distribution. That is, the unknown pixels are labelled either probable foreground or probable background. 
    * 우리가 제공한 데이터에 따라, GMM은 새로운 픽셀 분포를 배우고 만듭니다. 즉, 알 수 없는 픽셀은 가능한 전경 또는 가능한 배경으로 표시되어 있다. try to model foreground and background
    
5. A graph is built from this pixel distribution. Nodes in the graphs are pixels Additional two nodes are added, Source node and Sink node. Every foreground pixel is connected to Source node and every background pixel is connected to Sink node.
    * 그래프는 이 픽셀 분포로 만들어졌다. 그래프의 노드는 픽셀입니다. 소스 노드와 싱크 노드라는 두 개의 노드가 추가됩니다. 모든 전경 픽셀은 소스 노드에 연결되고 모든 배경 픽셀은 싱크 노드에 연결됩니다.
    
6. The weights of edges connecting pixels to source node/end node are defined by the probability of a pixel being foreground/background
    * 픽셀을 소스 노드/엔드 노드에 연결하는 가장자리의 가중치는 픽셀이 전경/배경일 확률로 정의됩니다.
    
7. The weights between the pixels are defined by the edge information or pixel similarity. If there is  a large difference in pixel color, the edge between them will get a low weight.
    * 픽셀 사이의 가중치는 가장자리 정보 또는 픽셀 유사성에 의해 정의된다. 픽셀 색상에 큰 차이가 있다면, 그들 사이의 가장자리는 무게가 낮을 것이다.
    
8. A minute algorithm is used to segment the graph. It cuts the graph into two separating source node and sink node with minimum cost function. The cost function is the sum of all weights of the edges that are cut.
    * 그래프를 분할하기 위해 분 알고리즘이 사용된다. 그것은 그래프를 최소 비용 함수로 두 개의 분리 소스 노드와 싱크 노드로 자른다. 비용 함수는 절단된 가장자리의 모든 가중치의 합이다.
    
9. After the cut, all pixels connected to Source node become foreground and those connected to Sink node become background.
    * 절단 후, 소스 노드에 연결된 모든 픽셀은 전경이 되고 싱크 노드에 연결된 픽셀은 배경이 된다.
    
10. The process is continued until the classification converges.
    * 그 과정은 분류가 수렴될 때까지 계속된다.
