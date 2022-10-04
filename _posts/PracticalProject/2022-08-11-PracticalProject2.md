---
layout: single
title: \[예습] HTML Form
toc: true
toc_sticky: true
categories: Practical
published: true
---

# HTML Form
사용자의 데이터를 서버에 전송하는 방법
* 로그인
* 회원가입
* 글 작성, 파일 업로드 등

## Form 동작원리

Form<br/>
Webpage <-> Web Server <-> Web program <-> DB<br/>
**Submit**

## Form 기본구조

```
<form action=“form_ok.php” method=“post”>

  <label for “uname”>이름:</label><br>
  <input type=“text” id=“uname” name = “uname”
placeholder=‘이름을 입력’><br>

  <label for=“email”>이메일:</label><br>
  <input type=“text” id=“email” name=“email”><br>
<br>

   <input type=“submit” value=“Submit”>
</form>
```
> 반드시 input에는 **uname**을 지정<br/>
> **placeholder**: 텍스트 input에 나오는 힌트글<br/>
> **submit**: 데이터를 서버로 전송

## Form 태그 속성

* **action**: 폼 데이터를 전송하면 받는 서버쪽 파일 지정
* **method**: 폼을 서버에 전송하는 메소드 종류
    * get/post
* name: 폼 이름 식별자
* target
    * action 파일을 현재 창이 아닌 다른 창에서 열도록 할 때 지정
* enctype
    * 폼 데이터가 서버에 전송할 때 인코딩 되는 방식
    * 파일 전송시 사용
    * ```enctype=“multipart/form-data”```

### Form method: Get/Post
* **GET**
    * Default
    * URL에 폼 데이터가 포함되어 전송<br/>
      <img width="380" alt="스크린샷 2022-08-11 오전 2 57 42" src="https://user-images.githubusercontent.com/63464299/184079899-d330de13-5471-4f27-97f8-16952dd7db95.png">
    * 전송할 수 있는 정보 길이가 제한
    * 퍼머링크(permalink, 고유한 주소체계)로 사용가능
* **POST**
    * 폼 데이터는 header의 body에 담겨 전송
    * URL에 정보가 표시되지 않음
    * 전송할 수 있는 데이터 길이 제한이 없음(장문의 데이터)
    * GET 방식 보다 보안성이 높음

## Form Elements
* **&#60;fieldset&#62; &#60;legend&#62;** tag
    * **fieldset**: 폼 엘리먼트 그룹화
    * **legend**: 그룹화한 폼 엘리먼트의 이름지정
    
```
<form action=“save_ok.php” name=“person” method=“post”>
    <fieldset style=‘width:200px;margin:5px’>
	<legend>개인 정보 입력</legend>	
	이름 : <input type = “text” name = “name” /><br><br>
	이메일 : <input type = “text” name = “email” /><br><br>
    </fieldset>
    <input type=‘submit’ value=‘저장’> <input type=‘reset’ value=‘취소>
</form>
```
* **&#60;input&#62;** tag
    * 폼 태그 내에 다양한 모양으로 입력할 수 있는 엘리먼트 제공
    * type 속성
        * **text, password, button, hidden, file**
        * **radio**
            * <u>한 그룹으로 묶이는 엘리먼트들에 한해 name을 동일</u>, value는 다르게
	* **checkbox**
	    * <u>php의 경우, name을 다르게</u>. 같게할 수 있지만 jsp나 spring의 가공 필요
        * **submit**
            * 폼에 입력한 데이터를 서버로 전송
            * ```<input type= ‘submit’ value=‘저장’>```
        * **reset**
            * 폼안에 있는 엘리먼트의 값을 초기화
            * ```<input type= ‘reset’ value=‘취소’>``` 
    * name: 엘리먼트 이름
    * id: 엘리먼트 id
    * readonly: 읽기 전용
    * maxlength=10: 입력 글자수 개수 지정
    * html5에 추가된 속성
        * **required**(필수입력)
        * **autofocus**(첫 포커스)
        * **placeholder**(입력 엘리먼트 힌트)
        * **pattern**(정규표현식 사용)
* **&#60;select&#62;, &#60;optgroup&#62;, &#60;option&#62;** tag
    * 목록 중의 항목을 선택
    * **multiple(다중선택)**, **selected(선택된 항목)** 속성 제공
    
```
지역선택 :
<select name=“city”>
	<optgroup label=“서울”>
		<option value=“1”>강남구</option>
		<option value=“2”>서초구</option>
		<option value=“3”>송파구</option>
	</optgroup>
	<optgroup label=“경기도”>
		<option value=“11”>성남시</option>
		<option value=“12”>수원시</option>
		<option value=“13”>용인시</option>
	</optgroup>
</select>
```

* **&#60;textarea&#62; contents &#60;/textarea&#62;** tag
    * 여러 줄의 텍스트를 입력
    * **rows**, **cols** 속성 제공
    
```
제목 : <input type=‘text’ name=‘subject’><br>
내용 :<br>
<textarea name=‘content’ cols=40 rows=5></textarea>
```

* **html5** 추가
    * **&#60;datalist&#62;** tag
        * 텍스트 입력 엘리먼트 
        * 클릭하면 후보 목록을 제공
        * text + option 기능
    * **&#60;input&#62;** tag
        * 시간관련 type 추가
            * date, month, week, time, date time 등 추가
            * ```<input type='date' min='2019-01-01' max='2020-12-31' name='fromdate'>```
        * 숫자 입력 type 추가
            * number, range 추가
        * color type 추가
            * ```<input type='color' name='color' value='#ff0000'>```
