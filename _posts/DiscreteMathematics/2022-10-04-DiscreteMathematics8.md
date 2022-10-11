---
layout: single
title: Summations & Cardinality & Matrices
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Summations
## Summations
* Sum of the terms<br/>
<img width="215" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193803819-fe0da519-1f43-484a-8890-523bc7e69a44.png">
  * Notation<br/>
    <img width="226" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193803861-6d7f8d3e-2673-490f-8bba-c95e69acb5ee.png">
	* Represent<br/>
	  <img width="115" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/195079180-fc73803d-e0fa-4b46-bed3-2eb0a47b6bea.png">
    * variable j: **index of summation**
    * m: **lower limit**
    * n: **upper limit** 
  * for a set S<br/>
    <img width="47" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193804111-aec9374b-37e1-430a-bf5b-e2c93c455510.png">

	  * If S = {2, 5, 7, 10} 
	  * a2 + a5 + a7+ a10 ≠ 2 + 5 + 7 +10
	  * S: a set of indices
 
## Geometric Series
* Sums of terms of geometric progressions(등비수열)<br/>
<img width="159" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193804211-43ec82a9-db65-4a89-a936-d4e0e8bee082.png">

------------


# Cardinality

## Cardinality of Sets
* Cardinality
	* \|A\| = \|B\| ↔︎ one-to-one correspondence(bijection)
* Countable
	* finite set
	* infinite set (**Countably infinite**)
		* 양의 정수(Z+) 집합과 같은 cardinality를 갖는 무한 집합
		* ↔︎ 무한 집합 중에서 자신의 원소들을 양의 정수로 index를 달면서 순서대로 나열할 수 있는 경우
		* ℵ0 (aleph): countably infinite’s cardinality
		* |\S\| = ℵ0 : aleph null

## Showing that a Set is Countable
* 집합이 countable임을 증명
	* f is a one-to-one correspondence(bijection) from N to a set S
		* show that it is one-to-one
			* f(n) = f(m) -> n = m
		* show that it is onto
			* f(x) = y

## Countable Sets and Uncountable sets
* Countable Sets
	* set of finite strings = countably infinite
	* set of all Java programs
	* the positive rational numbers(유리수)
* Uncountable sets
	* the real numbers(실수) (R)

--------------

# MATRICES

## Illustration of Matrix Multiplication
<img width="222" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805050-4ea26ffe-e6c3-43d1-bcbc-f48c6811c9ee.png"><br/>
<img width="184" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805116-afdcb7a0-f352-484b-a407-0037af68d0f2.png">

## Identity Matrix and Powers of Matrices
* Identity Matrix (항등 행렬)
	* 주대각선의 원소가 모두 1이며 나머지 원소는 모두 0인 정사각 행렬
* Powers of square matrices
	* A^0 = In
	* A^r = A*A*A…A (r times)

## Transposes of Matrices
* <img width="52" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805283-339d55a4-b10e-4235-a41b-4ccee2b185e9.png">: m x n matrix
* Transpose of A
	* <img width="13" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805330-66928372-88f0-4422-b942-51be1e91083f.png">: n x m matrix
* <img width="126" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805372-ec6c9eab-219d-49ff-8bdf-f5a009135d0d.png">

	* for i = 1, 2, … , n and j = 1, 2, …, m

<img width="257" alt="스크린샷 2022-10-04 오후 7 45 38" src="https://user-images.githubusercontent.com/63464299/193805461-b91ce437-f917-4ade-88b3-a8bb93102a7c.png">

* square matrix A<br/>
<img width="40" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805524-f23d087c-700c-461e-bf0b-783c84d9feb8.png"> → symmetric
* <img width="200" alt="알 수 없음" src="https://user-images.githubusercontent.com/63464299/193805600-9ff9bb97-1f5b-41a4-8613-a384bc05b6e1.png">	
	* for i and j with 1≤i≤n and 1≤j≤n
	 ![Pasted Graphic 12](https://user-images.githubusercontent.com/63464299/193809135-115869bc-94fe-44d9-9579-4674cd10d711.png)

## Zero-One Matrices
* zero-one matrix
	* 모든 항목이 0 or 1
	
![Pasted Graphic 13](https://user-images.githubusercontent.com/63464299/193806269-81e6d38d-aec9-4dd1-affa-48807c7a25c0.png)



## Joins and Meets of Zero-One Matrices
* Joins and Meets<br/>
![Pasted Graphic 14](https://user-images.githubusercontent.com/63464299/193806401-86b24872-fd78-44a9-86f5-d43d9f9b6d1c.png)
	* The join of A and B<br/>
	  ![Pasted Graphic 15](https://user-images.githubusercontent.com/63464299/193806504-522fc03e-e3c2-4704-ac9c-d548473d8d4c.png)

	* The meet of A and B<br/>
	  ![Pasted Graphic 16](https://user-images.githubusercontent.com/63464299/193806661-fd6fef1e-ea90-4187-9d90-f9f87e307076.png)

## Boolean Product of Zero-One Matrices
* A = [aij] : m x k zero-one matrix
* B = [bij] : k x n zero-one matrix
* The Boolean product of A and B
	* A ⊙ B : m x n zero-one matrix 

![Pasted Graphic 17](https://user-images.githubusercontent.com/63464299/193806882-db706aee-d65b-492b-bd2c-fb2bd6d06d40.png)
* Ex)<br/>
 ![Pasted Graphic 18](https://user-images.githubusercontent.com/63464299/193807041-3cb3d2d1-87a5-41bd-bb8b-9a2ea1d48a4c.png)


