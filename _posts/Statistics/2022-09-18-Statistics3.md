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
* 양적자료의 중심위치의 측도로 가장 많이 사용
* 모평균 : 상수
* 표본평균: 변수

## 가중평균(weighted mean)
* 평균(측정값 x 가중치)
* 성적평점평균 or 물가지수
* <img width="108" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910653-8d5da838-e8f1-4e7b-9ecd-c856a2d41d8b.png">

## 이상치(outlier)
* 주종을 이루는 값에 비해 아주 큰 값이거나 아주 작은 값

## 중앙값(median)
* 양적자료를 나열했을 때 가운데 위치하는 값
* n: 홀수 => (n+1)/2
* n: 짝수 => Avg(n/2, n/2+1)
* 이상치에 민감x(가운데값은 일정)

## 최빈값(mode)
* 빈도(도수)가 가장 많은 값
* 최빈값이 없거나 하나 이상의 최빈값을 가짐
* 평균, 중앙값: 하나의 값, 양적자료에만 사용
* 최빈값: 질적 자료, 양적 자료 모두 사용
* 양적자료: 가장 도수가 높은 계급의 중간값

## 평균, 중앙값과 최빈값의 관계
1. Unimodal, Symmetry Histogram or 도수분포곡선
	* 평균 = 중앙값 = 최빈값 = 분포의 중간
2. skewed to the right Histogram or 도수분포곡선
	* 평균 > 중앙값 > 최빈값
3. skewed to the left Histogram or 도수분포곡선
	* 평균 < 중앙값 < 최빈값

## 절사평균(trimmed mean)
* 가장 작은 값과 가장 큰 값을 제한 나머지의 평균

## 산포(dispersion)
* 자료의 흩어짐에 대한 측도
* 평균은 같지만 산포가 다를 수 있다!

## 범위(range)
* 최대값 - 최소값
* 이상치에 민감 (범위가 커지면 이상치도 커짐) -> 정확한 정보 확신x


## 분산과 표준편차(variance and standard deviation)
* 자료의 값들이 평균을 중심으로 얼마나 퍼져 있는가를 나타내는 측도
* 편차(deviation)
* 관찰값 - 평균
* 분산, 표준편차 >= 0
* 변동이 1도 없을경우 0
* 분산의 측도단위는 원자료의 측도단위의 제곱
* 표준편차의 측도단위는 원자료의 측도단위

-------------

# 자료의 산포도

## 모분산과 표본분산
* 모분산:<br/>
    <img width="68" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910664-e37cbbab-65d8-4d44-962f-43eb2d8c6434.png">

	* 분산의 간편식:<br/>
	    <img width="70" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910674-09c082be-9011-4d61-bcd1-80d613523089.png">

* 표본분산:<br/>
    <img width="80" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910690-da5c6146-634e-4d93-a4e9-f8a72d590251.png">

	* 분산의 간편식:<br/>
    	    <img width="68" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910700-9a09f8d6-7fce-42a4-b48a-36ddf0af8fa8.png">
	* n 대신 n-1
    
* 모표준편차:<br/>
    <img width="31" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910712-496fdc48-a948-46c1-8c32-45412d4c7f65.png">

* 표본표준편차:<br/>
    <img width="28" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910736-c3bdeb6e-8cec-4176-8d28-85fec62e3adb.png">

* 모수 (population parameter): 모집단에서 계산된 <u>측도</u>(평균, 중앙값, 최빈값, 범위, 분산, 표준편차)
	* 𝜇, 𝝈
* 통계량 (statistic): 표본자료에서 계산된 측도
      * <img width="5" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910767-a542cc82-18b8-4a08-9bf2-62de4d67d31c.png">, s

## 변동계수(coefficient of variation, CV)
* 자료 간에 자료값의 차이가 큰 경우(주별↔︎월별), 측정 단위가 다른 경우 산포를 비교할 때 사용
* multiple 100%
* 변동계수(모집단):<br/>
      <img width="55" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910802-e07d94e4-753f-4937-bd4c-c49d565cec7f.png">
      
* 변동계수(표본집단):<br/>
      <img width="55" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910810-dddeef92-fcad-4e7c-816c-4f6b9d7953e3.png">

-------------

# 집단화된 자료의 평균, 분산과 표준편차

## grouped data(집단화된 자료)의 평균
* 합의 근사치를 구하여 집단화된 자료의 평균을 구함
* m: 각 계급의 중앙값
* f: 각 계급의 빈도(도수)
* 모평균:<br/>
      <img width="34" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910839-c6e4b6b5-f093-4e4e-8e19-8bec3f856d54.png">

* 표본평균:<br/>
      <img width="34" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910851-c7a6fb4a-1dd5-40ff-9979-3eec3e66bd76.png">

## grouped data의 분산과 표준편차
* 모분산:<br/>
      <img width="66" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910866-17e5d678-ee29-4046-8316-904a7420a1f5.png">

	* 분산의 간편식:<br/>
      		<img width="84" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910876-a5ce6558-a9e7-4157-960c-9979a53704e0.png">

* 표본분산:<br/>
      <img width="65" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910886-578e15f8-db8f-43e8-a18f-7a6d16ae473a.png">
	
	* 분산의 간편식:<br/>
      		<img width="82" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/190910898-aebb67ee-add3-40d1-ab96-69b749cfa949.png">

-----------

# 표준편차의 이용

## 체비셰프의 정리(Chebyshev’s theorem)
* 평균과 표준편차를 이용해 평균에 대해 주어진 구간에 들어가는 관측치의 비율을 구함
* 어떠한 k>1에 대해서, 자료중 적어도 100(1-1/k^2)가 평균으로부터 표준편차의 k배 이내에 있다.
* k=2: 적어도 75%가 평균으로부터 표준편차의 2배 이내에 있음
* k=3: 적어도 89%가 평균으로부터 표준편차의 3배 이내에 있음

## 경험적 규칙(empirical rule)
* 자료의 분포가 평균을 중심으로 좌우 대칭이고 종을 엎어 놓은 모양인 경우에 좀 더 정확한 결과를 얻을 수 있는 규칙
* 자료의 분포: Unimodal, Symmetry 인 경우
* x-bar(표본평균)±s(표본표준편차): 관측 값의 약 68%
* x-bar±2s: 관측 값의 약 95%
* x-bar±3s: 관측 값의 약 99%
* 체비셰프의 정리 보다 더 정확


## 백분위수(percentile)
* 크기 순서로 나열한 자료를 100등분한 측도

-----------

# 상대적 위치의 측도

## 사분위수(quartile)
* 크기 순서로 나열한 자료를 4등분한 측도
* 제1사분위수: Q1 = 25 percentile
* 제2사분위수: Q2 = 50 percentile = median(중앙)
* median 값: 이상치의 영향을 받지 않는 값
* 제3사분위수: Q3 = 75 percentile

## 사분위범위(interquartile range: IQR)
* 제3사분위수 - 제1사분위수 (IQR = Q3 - Q1)

-----------

# 상자그림

## 상자그림(box plot)
* 자료의 중앙값, 제1사분위수, 제3사분위수, 아래 울타리(Q1-1.5*IQR), 위 울타리(Q3+1.5IQR) 사이에 있는 자료의 최솟값, 최대값 등을 이용하여 자료의 정보를 그림으로 나타낸 것
* 아래 울타리: Q1 - 1.5IQR
* 위 울타리: Q3 + 1.5IQR
* outer fence: 3IQR 이상, 이하
* 3IQR 안: mild outlier
* 3IQR 밖: extreme outlier
* 경계안의 symbol이 다름
