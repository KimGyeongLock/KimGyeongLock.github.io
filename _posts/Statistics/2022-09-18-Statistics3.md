---
layout: single
title: 3장 기술통계
toc: true
toc_sticky: true
categories: Statistics
published: true
---

# 자료의 중심위치의 측도

## 평균(mean)
* 산술평균
* **양적자료**의 중심위치의 측도로 가장 많이 사용
* 이상치에 민감
* **모평균**: 상수<br/>
<img width="64" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190959297-0bc9d593-7ef0-4869-a772-6e6248de56a3.png">
* **표본평균**: 변수<br/>
<img width="64" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190959349-22224212-33d6-4348-ab34-b3bfee5fddb4.png">

## 가중평균(weighted mean)
* **총합(각값x가중치)/가중치의합**
* 성적평점평균 or 물가지수
* <img width="108" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910653-8d5da838-e8f1-4e7b-9ecd-c856a2d41d8b.png">

## 이상치(outlier)
* 주종을 이루는 값에 비해 아주 큰 값이거나 아주 작은 값

## 중앙값(median)
* 양적자료를 나열했을 때 가운데 위치하는 값
* n: 홀수 => **(n+1)/2**
* n: 짝수 => **Avg(n/2, n/2+1)**
* 이상치에 민감x(가운데값은 일정)
* 한두 개의 데이터만 사용하기 때문에 많은 정보를 놓칠 수 있

## 최빈값(mode)
* 빈도(도수)가 가장 많은 값
* 최빈값이 없거나 하나 이상의 최빈값을 가짐
* 평균, 중앙값: 하나의 값, **양적자료에만** 사용
* 최빈값: **질적 자료, 양적 자료 모두** 사용
	* 양적자료 - 가장 도수가 높은 계급의 중간값

## 평균, 중앙값과 최빈값의 관계
1. **Unimodal, Symmetry** Histogram or 도수분포곡선
	* 평균 = 중앙값 = 최빈값 = 분포의 중간
2. **skewed to the right** Histogram or 도수분포곡선
	* 평균 > 중앙값 > 최빈값
	* Ex) 소득분포
	
3. **skewed to the left** Histogram or 도수분포곡선
	* 평균 < 중앙값 < 최빈값
	* Ex) 수능시험성적
	
* 산술평균: 무게중심, 중앙값: 면적의 50%<br/>
  분포가 바뀌면 무게중심을 바뀌지만 면적은 거의 안 바뀐다.

## 절사평균(trimmed mean)
* **평균(전체 - (가장 큰값, 가장 작은값))**
* 아이스 댄싱, 체조, 수영, 피겨스케이팅 경기에서 사용
* Ex) 8 - 2 => 1/8-trimmed mean<br/>
	12 - 2 => 1/12-trimmed mean

## 산포(dispersion)
* 자료의 흩어짐에 대한 측도
* 평균은 같지만 산포가 다를 수 있다!

## 범위(range)
* **최대값 - 최소값**
* 이상치에 민감 (범위가 커지면 이상치도 커짐) -> 정확한 정보가 아닐 수 있음


## 분산과 표준편차(variance and standard deviation)
* 자료의 값들이 평균을 중심으로 얼마나 퍼져 있는가를 나타내는 측도
* **편차(deviation)**
	* **관찰값 - 평균**
	* 모든 편차의 합은 0
* 분산, 표준편차 >= 0
* 변동이 1도 없을경우 분산, 표준편차 = 0
* 분산의 측도단위는 원자료의 측도단위의 <u>제곱</u>
* 표준편차의 측도단위는 원자료의 측도단위

-------------

# 자료의 산포도

## 모분산과 표본분산
* **모분산**:<br/>
    <img width="120" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960304-687d4526-2491-4c03-8e98-7cb2173faac8.png">

	* 분산의 간편식:<br/>
	    <img width="115" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960322-2b5885f3-6b86-4729-98ea-e178776ee41a.png">

* **표본분산**:<br/>
    <img width="139" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960328-78ec457f-3006-463a-a81a-51d840db4adb.png">

	* 분산의 간편식:<br/>
    	    <img width="113" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960340-b5ab21d4-0b12-49da-a564-1c7db07ea31d.png">
	* n 대신 **n-1**로 나눔
    
* **모표준편차**:<br/>
    <img width="53" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960354-5a5484b7-39fd-4c45-a842-250e59ab63ce.png">

* **표본표준편차**:<br/>
    <img width="49" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960370-9acde87c-2232-4bc7-aea7-64fc916e5eaa.png">

* **모수(population parameter)**
	* 모집단에서 계산된 <u>측도</u>(평균, 중앙값, 최빈값, 범위, 분산, 표준편차)
	* 𝜇, 𝝈
* **통계량(statistic)**
	* 표본자료에서 계산된 측도
	* <img width="5" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910767-a542cc82-18b8-4a08-9bf2-62de4d67d31c.png">{: width="10" height="10"}, s

## 변동계수(coefficient of variation, CV)
특정상황에서 산포를 비교할 때 사용
* 자료 간에 자료값의 차이가 큰 경우(어른의 몸무게, 신생아의 몸무게)
* 측정 단위가 다른 경우(키와 몸무게, 주별,)
<br/>
* x 100%
* **변동계수(모집단)**:<br/>
      <img width="97" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960611-f04cc86a-0ee9-426e-bfa9-a9bf5a1daf66.png">
      
* **변동계수(표본집단)**:<br/>
      <img width="96" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190960632-0d055614-da1e-449b-af4f-dff5d441dc3f.png">

-------------

# 집단화된 자료의 평균, 분산과 표준편차

## grouped data(집단화된 자료)의 평균
* 합의 **근사치**를 구하여 집단화된 자료의 평균을 구함
* m: 각 계급의 중앙값
* f: 각 계급의 빈도(도수)
* 모평균:<br/>
      <img width="59" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962744-db87d059-7643-4394-9a7b-fd72a9645c39.png">

* 표본평균:<br/>
      <img width="59" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962761-102b7891-e159-4d3c-b064-b76b10b7e38b.png">

## grouped data의 분산과 표준편차
* 관찰값 대신 계급의 중앙값(m)을 
* 모분산:<br/>
      <img width="115" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962772-d37dfaeb-31f5-4ce1-a4e2-d9b64c44ef64.png">

	* 분산의 간편식:<br/>
      		<img width="145" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962784-8772764a-3c95-47d3-b5b9-9e29b8b48201.png">

* 표본분산:<br/>
      <img width="113" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962801-4550f78e-1fdb-4f10-ab55-0feab2f1dcdc.png">
	
	* 분산의 간편식:<br/>
      		<img width="143" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190962815-5c32310f-4034-4fec-b1c2-44e014f498a1.png">

-----------

# 표준편차의 이용

## 체비셰프의 정리(Chebyshev’s theorem)
* 평균과 표준편차를 이용해 평균에 대해 주어진 구간에 들어가는 **관측치의 비율**을 구함
* 어떠한 k>1에 대해서, 자료중 적어도 **100(1-1/k^2)**가 평균으로부터 표준편차의 k배 이내에 있다.
	* k=2: 적어도 75%가 평균으로부터 표준편차의 2배 이내에 있음
	* k=3: 적어도 89%가 평균으로부터 표준편차의 3배 이내에 있음

## 경험적 규칙(empirical rule)
* 자료의 분포: Unimodal, Symmetry 인 경우 -> 좀더 정확한결과
* x-bar(표본평균)±s(표본표준편차): 관측 값의 약 **68%**
* x-bar±2s: 관측 값의 약 **95%**
* x-bar±3s: 관측 값의 약 **99%**
* 체비셰프의 정리 보다 더 정확


## 백분위수(percentile)
* 크기 순서로 나열한 자료를 100등분한 측도
* **1 + p(n-1)**
* p: 백분율
	* Ex) 60번째 백분위수의 위치<br/>
		**1+p(n-1)** = 1 + 0.6x(20-1) = 12.4<br/>
		=> k = 12, d = 0.4<br/>
		**xk + d x (x(k+1) - xk)** = x12 + 0.4 x(x13-x12)<br/>
		10.4 + (0.4)(0) = 10.4

-----------

# 상대적 위치의 측도

## 사분위수(quartile)
* 크기 순서로 나열한 자료를 4등분한 측도
* **제1사분위수**: Q1 = 25 percentile
* **제2사분위수**: Q2 = 50 percentile = median(중앙)
	* median 값: 이상치의 영향을 받지 않는 값
* **제3사분위수**: Q3 = 75 percentile

* Ex) Q1: 1 + p x (n-1) = 1 + 0.25x14 = 4.5 -> x4 + dx(x5 - x4)<br/>
	Q2: p = 0.5, Q3: p = 0.75
 
## 사분위범위(interquartile range: IQR)
* **제3사분위수 - 제1사분위수** (IQR = Q3 - Q1)

-----------

# 상자그림

## 상자그림(box plot)
* 자료의 중앙값, 제1사분위수, 제3사분위수, 아래 울타리(Q1-1.5*IQR), 위 울타리(Q3+1.5IQR) 사이에 있는 자료의 최솟값, 최대값 등을 이용하여 자료의 정보를 그림으로 나타낸 것
* 아래 울타리: Q1 - 1.5IQR (inner fence)
* 위 울타리: Q3 + 1.5IQR (inner fence)
* outer fence: 3IQR 이상, 이하
* 3IQR 안: mild outlier
* 3IQR 밖: extreme outlier
* 경계안의 symbol이 다름
