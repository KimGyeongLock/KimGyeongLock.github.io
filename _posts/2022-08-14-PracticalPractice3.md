---
layout: single
title: \[예습] HTML Form CSS, JS
toc: true
toc_sticky: true
categories: Practical
published: true
---

# CSS Forms
```
input[type=text] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}
```

1. input1 
```
input[name=input1] {
  border: 1px solid red;
 	border-radius: 10px;
}
input[name=input1]:focus {
	background-color: pink;
}
```
> Focus 전<br/>
> <img width="699" alt="스크린샷 2022-08-14 오후 6 13 18" src="https://user-images.githubusercontent.com/63464299/184535647-ed2b5505-e96e-48c8-bd08-2874eb036292.png"><br/>
> Focus 후<br/>
> <img width="703" alt="스크린샷 2022-08-14 오후 6 14 50" src="https://user-images.githubusercontent.com/63464299/184535740-ed4d50da-7620-4448-a48f-397fd7981abd.png">

2. input2
```
input[name=input2] {
	border: none;
  border-bottom:4px solid blue;
  background-color:skyblue;
}
```
> <img width="701" alt="스크린샷 2022-08-14 오후 6 13 45" src="https://user-images.githubusercontent.com/63464299/184535662-54698a7f-8919-463b-8397-7e77fc515efc.png">
  
3. input3
```
input[name=input3] {
	width:200px;
  transition:width 0.4s ease-in-out;
}
input[name=input3]:focus {
	width: 100%
}
```
> Foucs 전<br/>
> <img width="203" alt="스크린샷 2022-08-14 오후 6 14 10" src="https://user-images.githubusercontent.com/63464299/184535700-ec7e2a88-02f1-4443-a699-0f4f5f47661b.png"><br/>
> Focus 후<br/>
> <img width="704" alt="스크린샷 2022-08-14 오후 6 14 33" src="https://user-images.githubusercontent.com/63464299/184535722-660c3b5c-5a8c-4b72-857f-cc64de3e0947.png">

--------

# JavaScript Forms
* 인터프리터(interpreter) 언어로 웹 브라우저에 의해 해석되고 실행
* 타입이 없으며, 객체 지향형과 함수 프로그래밍 모두 가능
* 다른 페이지로 이동 및 **HTML 엘리먼트와 콘텐츠의 추가 또는 제거**
* **HTML 엘리먼트 스타일 변경**
* 폼의 유효성 검증
* 사용자와의 상호작용(마우스와 키보드 이벤트)에 대한 스크립트 실행
* **웹 브라우저 제어**, 쿠키 등의 설정과 조회
* AJAX 기술을 이용한 웹 서버와의 통신
* 동적인 효과 이미지 롤오버 상태표시줄에 문자열 표시 등등

JavaScript Tutorial: <https://www.w3schools.com/js/default.asp>

## Ex) 덧셈 계산기
<img width="150" alt="스크린샷 2022-08-14 오후 6 49 28" src="https://user-images.githubusercontent.com/63464299/184537245-2db6d112-cc82-45d3-b2a8-a159faa7e910.png">
<br/>
* **HTML**
	```
	<h4>덧셈 계산기</h4>
	<form>
		<input type="text" size=2 name="num1" id="num1" pattern="\d*"> 
		+
		<input type="text" size=2 name="num2" id="num2" pattern="\d*">
		<button onclick="add()" type="button"> = </button>
		<input type="text" size=2 name="result" id="result" readonly>
		<br><br>
		<input type="reset" value="초기화">
	</form>
	```
	> pattern=**“\d*”**: 숫자로 입력
	> add() 함수를 Javascript로 구현

* **JavaScript**
	&#60;**script**&#62; 태그 사용
	```
	<script>
		function add() {
  	  		var num1 = document.getElementById("num1");
  	      		var num2 = document.getElementById("num2");
        
  	      		var sum = parseInt(num1.value) + parseInt(num2.value);
        
  	      		var result = document.getElementById("result");
 	       		result.value = sum;
  	 	}
	</script>
	```
	> **document**: body안에 있는 모든 Elements
	> **.getElementByID**: ID로 Element를 찾아서 가져오기
	> **parseInt()**: 정수형 변환

# JavaScript Events
```<element event=‘javascript codes’ />```
* 이벤트 종류
    * **onchange**: 현재 요소 내용 변경 이벤트
    * **onclick**: 엘리먼트 클릭 이벤트
    * **onmouseover**: 엘리먼트 위에 마우스 올려질 때
    * **onmouseout**: 마우스가 엘리먼트 위에 있다가 다른 곳으로 이동할 때
    * **onkeydown**: 키보드 입력할 때
    * **onload**: 웹페이지 로딩 완료될 때
    * …

# JS Form Validation
* **HTML**
	```
	<form name=form1 action=form2_ok.php onsubmit="return validateForm()" method="post">
 		제목: <input type="text" name="subject"><br>
 		이름: <input type="text" name="writer"><br>
		내용: <textarea name="content" cols="20" rows="5"></textarea><br>
 		<input type="submit" value="저장">
	</form>
	```
	> **onsubmit**: 폼의 submit 버튼이 눌려질 때
* **JavaScript**
	```
	<script>
		function validateForm() {
    			var subject = document.form1.subject;
        		if (subject.value == "") {
        			alert("제목을 입력하세요");
            			subject.focus();
            			return false;
        		}
        
        		var writer = document.form1.writer;
        		if (writer == "") {
        			alert("이름을 입력하세요");
            			writer.focus();
            			return false;
        		}
        
        		if (writer.length < 2) {
        			alert("이름을 2글자이상 입력하세요");
            			writer.focus();
            			return false;
        		}     
    	}
	</script>
	```
	> Requirement: 
  > 제목을 반드시 입력<br/>
  > 이름을 반드시 입력<br/>
  > 이름은 2글자 이상 입력


# 전송 데이터 처리

* **form2_ok.php**
	```
	<?php
		$subject = $_POST[‘subject’];
		$writer = $_POST[‘writer’];
		$content = $_POST[‘content’];
	?>
	<!DOCTYPE html>
	<html lang=“en”>
	<head>
		<meta charset=“UTF-8”>
		<meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
		<title>Document</title>
	</head>
	<body>
		<h3>입력하신 데이터는 다음과 같습니다.</h3>
		<div>제목 : <?= $subject?> </div>
		<div>이름 : <?=$writer?> </div>
		<div>내용 : <?=$content?> </div>
	</body>
	</html>
	```
  > 폼에서 만든 **name**과 php에서 받아온 **name**은 동일
  > php에서 변수를 만들 때 맨 앞에 **$**를 추가
  > 화면에 출력을 할 때 **<?=** $subject**?>**

