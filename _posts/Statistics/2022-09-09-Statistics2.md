---
layout: single
title: 2장 표와 그림을 통한 자료의 요약 
toc: true
toc_sticky: true
categories: Statistics
published: true
---

# 데이터의 요약과 표현
## 데이터의 요약
* **확률변수 (random variable)**
    * **확률적 현상**
        * 결과를 미리 알 수 없는 상태에서 일어나는 현상
    * **확률변수**
        * 변수의 값이 확률적으로 정해지는 변수
        * **Xi**으로 표시(X1, X2, X3..)
        * 값: 정수(주사위) 혹은 실수(키)
* **확률 분포**
    * 확률변수의 다양한 가능한 값들이 흩어진 모양
    * 확률변수 x가 특정한 값을 가질 확률을 나타내는 분포
* **랜덤 표본(random sample)** 
    * X1, X2,… Xn(확률변수랑 표기 같음)
* **통계량**(statistic)
    * 랜덤표본을 수식으로 표현
    * X1+X2, X1-X2, X1X2(**대문자**)
        * 소문자: 상수, 정해져있는 값 관찰값
* 데이터(data)
    * 일변량 데이터(univariate data)
        * 한 변수만 측정 (xi)
    * 이변량 데이터(bivariate data)
        * 두 변수만 측정 (xi, yi)
    * 다변량 데이터(multivariate data)
        * 두 변수이상 측정

## 데이터의 표현
* 표(table)
  * 주로 질적 데이터의 요약에 사용
* **도수(frequency)**
  * 값이 나타난 횟수
* **상대도수(relative frequency)**
  * 도수 / 전체 데이터 수
* **누적상대도수(Cumulative relative frequency)**
* **도수분포(frequency table)**<br/>

|학위|도수|상대도수|누적 상대도수|
|:---:|:---:|:---:|:---:|
|학사|2000|0.80|0.80|
|석사|400|0.16|0.96|
|박사|100|0.04|1.0|

> 범주형 데이터<br/>
> 순서가 있는 데이터 -> **순서척도** 사용 -> 누적상대도수가 의미가 있음(순서대로 쌓임)

### 심슨의 역설(Simpsons’s Paradox)
* 범주형 데이터의 경우 **변수를 더 나누지 않고** 합쳐서 표를 작성함으로써 사실이 왜곡되는 것

--------------

# 질적 데이터의 그래프 표현
* **막대 그래프**(bar chart)
    * **명목척도**로 측정한 데이터 (or **순서척도**)
    * 가로축의 분류 항목끼리 **붙거나 떨어져도 관계x**
    * 막대의 넓이 = **도수의 비율**
    * 세로로 그려도됨, 막대 대신 아이콘 사용도됨
    * **막대를 중간에 잘라버리면 비율이 달라짐 (0점부터 시작해야함)**
* **원 그림**(pie chart)
    * 변수 별 데이터의 비율
    * 비율은 중심각에 비례

--------------

# 양적 데이터의 정리
* **계급 경계값**
    * 계급의 상한값(포함)~그 다음 계급의 하한값(불포함) Ex) 160<= x <160
* **계급 크기(class size)**
    * 상한경계값 - 하한경계값
* **계급 중앙값(class midpoint)**
    * 하한값 + 계급크기 / 2
* **계급(class)**
    * 상한값과 하한값 사이에 들어가는 모든 값을 포함하는 구간(양적자료)
* **그룹화된 자료(grouped data)**
    * 도수분포표의 형식으로 정리된 자료
    * 구간별로 분류


## 도수분포표 작성 
1. 계급의 수
	: 자료의 수에 따라 사용자가 임의로 결정
2. 계급 크기
	: 모든 계급의 크기가 같아야 좋음
	근사적 계급크기 = (가장큰값 - 가장 작은 값) / 계급의 수(편의상)
3. 첫 번째 계급의 하한값 혹은 시작점 
	: 가장 작은 값 or 더 작은 값(0) = 첫 번째 계급의 하한값


## 히스토그램(histogram)
* **구간, 비율척도** 사용
* 가로축: 계급 (반드시 숫자)
* 세로축: 도수, 상대도수, 퍼센트, 백분위

![page9image9555408](https://user-images.githubusercontent.com/63464299/189329991-88b418ec-1f04-4eb4-8d20-993dd5e11b26.png){: width="200" height="200"}

### 히스토그램 그릴 때 주의 사항
1. **구간/비율척도**로 측정한 데이터 사용
2. 가로축에 나타나는 값끼리는 붙어야한다(막대그래프랑은 다름)
3. 막대의 높이가 도수의 비율을 정확이 반영해야 분포를 볼 수 있다
4. 세로축에 두가지 다른 축을 동시에 표현하면 값의 변화를 왜곡하고 두 변화가 합쳐지는 것처럼 보임
5. 간격(bin)을 너무 좁게 잡으면 전체 분포를 파악하는데 어려움
   <br/>간격을 너무 넓게 잡으면 분포를 제대로 파악x
6. 히스토그램을 90도 돌리면 증가 추세가 오히려 감소추세로 보일 수 있음

### 히스토그램의 모양과 분포
* 대칭 히스토그램(symmetric histogram)
   * unimodal
   * bimodal
   
![page19image9511664](https://user-images.githubusercontent.com/63464299/189334218-65fd3a23-071a-4ff3-b5ce-864a5e0788cc.jpg){: width="200" height="200"}

* 한쪽으로 치우친 히스토그램(skewed histogram)
   * 오른쪽 꼬리 긴 히스토그램(skewed to the Right)
   * 왼쪽 꼬리 긴 히스토그램(skewed to the Left)

![page19image9515200](https://user-images.githubusercontent.com/63464299/189334251-cea2e313-3abe-4e2f-842a-49bf1617fde4.jpg){: width="200" height="200"}

 
 
## 도수다각형(frequency polygon)
* 히스토그램의 각 막대의 중앙을 직선으로 연결한 그래프

![page10image10175920](https://user-images.githubusercontent.com/63464299/189330119-6d6d39d4-5480-4701-911f-9b2f06fbcdd2.jpg){: width="200" height="200"}
 > skewed to right

## 도수분포곡선(frequency distribution curve)
* 자료의 수가 많아지고, 계급의 수가 증가하면 도수다각형이 부드러운 곡선이 됨

![page10image10189856](https://user-images.githubusercontent.com/63464299/189330267-1887162f-e5b6-46e8-8ff4-4b5f3b687324.jpg){: width="200" height="200"}

## 꺾은선 그래프(line chart)
* 데이터의 **시간에 따른 변화**를 나타내는데 사용
* 계절에 따른 변동
* (장기적) 추세
* 회전x -> 다른 느낌 반드시 시간: 
* 꺾은 선 그래프의 오류
    * 가로축을 늘리고 세로축을 줄이면 매우 느리고 변동이 좁은 것처럼 보임(vice versa)
    * 시간의 축 간격 일정!
    * 축을 중간에 끊어 버리면 축 간격이 값의 변화를 과장하거나 과소하여 표현가능주의
    
![10 - 120](https://user-images.githubusercontent.com/63464299/189330908-8f15e49e-455e-46b8-8929-1c2adfa75906.jpg){: width="200" height="200"}

 
## 인구피라미드
* 히스토그램 두개를 좌우로 회전하여 합친 것
* 두개를 한눈에 볼 수 있음

![page13image10801008](https://user-images.githubusercontent.com/63464299/189331556-6aec9f10-95c0-4e42-9d88-7d64375b7ed7.jpg){: width="200" height="200"}

## 레이더 차트(또는 별그림(star plot)
* 여러 부분에서 특성을 비교한 그림
* ex) 품질관리 분임조활동, 제품의 특성 비교

![MER IDD](https://user-images.githubusercontent.com/63464299/189331860-796bf38e-6555-4a85-8110-00ab49b63283.jpg){: width="200" height="200"}

## Face
* Herman Chernoff
* 다변량 데이터를 그림으로 나타냄
* 너무 많은 변수가 포함되어 읽어내기 어려움(가독성, 판독성이 떨어짐)

![Facial Plota On Four Standardired Social Impact Criteria](https://user-images.githubusercontent.com/63464299/189331892-ca9b71f4-1958-4c99-9415-a56a08ccfb7d.jpg){: width="200" height="200"}

 
## 줄기-잎 그림(stem-and-leaf displays)
* 왼쪽: 줄기 10단위
* 오르쪽: 잎 나머지 값을 일단 관찰된 순서대로 작성 -> 오름차순으로 재정렬

## 누적도수분포곡선(Ogive)
* 가로축: 각 계급의 상한값
* 세로축: 대응하는 누적도수
* 각 점들을 직선으로 연결하는 곡선

![page21image10153968](https://user-images.githubusercontent.com/63464299/189334504-4b9a9074-13b9-43e0-94e9-8568f82a20ff.jpg){: width="200" height="200"}

 
## 파레토 차트
* 품질관리에 주로 사용
* 빈도가 높은 것 순
* 명목 척도

![Chart Title](https://user-images.githubusercontent.com/63464299/189334648-8ce031d2-fe83-4aed-8764-a11fb8ab053b.jpg){: width="200" height="200"}
> 막대: 관찰 도수<br/>
> 주황색 선: 누적된 상대돗수(%)<br/>
> Price와 Packaging 항목이 70%를 차지


## 그래프를 그릴 때
1. 변량의 종류에 따라 그릴 수 있는지 여부
2. 나타내고자 하는 내용이 무엇인지
3. 축의 선정에 오류가 없는지
4. 가로축과 세로축의 비율이 적정한지
5. 특히 세로축을 절단함으로써 생길 오류가 있는지 여부를 확인
