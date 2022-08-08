---
layout: single
title: \[예습] 웹 서비스 개발
toc: true
toc_sticky: true
categories: Practical
published: true
---

# Web development

Full Stack
* **Front-end**<br/>
  사용자와 상호작용하는 화면
  * **HTML**<br/>
    **H**yper **T**ext **M**arkup **L**anguage
  * **CSS**<br/>
    **C**ascading **S**tyle **S**heets
  * **JS**(**J**ava**S**cript)<br/>
    change HTML content
  
* **Back-end**<br/>
  컨테츠나 자원들과 통신하는 모든 프로그램
  * 서버(OS)
  * 데이터베이스(Database)
  * Web Framework(Spring)
  * Programming Language(Java)

## Front-end
1. 컨텐츠 작성<br/>
<img width="483" alt="스크린샷 2022-08-08 오후 2 29 25" src="https://user-images.githubusercontent.com/63464299/183352377-724456ad-4eb0-4587-a966-509368614f12.png">
3. HTML: 레이아웃 배치<br/>
<img width="408" alt="스크린샷 2022-08-08 오후 2 32 17" src="https://user-images.githubusercontent.com/63464299/183352392-c766da34-40c1-4e2a-a707-1c808f524f34.png">
5. 각 영역에 컨텐츠 배치<br/>
<img width="402" alt="스크린샷 2022-08-08 오후 2 35 42" src="https://user-images.githubusercontent.com/63464299/183352407-ee6e87a9-d464-4443-849b-f4f6f27d104b.png">
7. CSS: 스타일<br/>
<img width="405" alt="스크린샷 2022-08-08 오후 2 54 20" src="https://user-images.githubusercontent.com/63464299/183352462-78207836-b9a0-4585-90f2-1d4baec0a36d.png"><br/>
<img width="384" alt="스크린샷 2022-08-08 오후 2 52 36" src="https://user-images.githubusercontent.com/63464299/183352476-9ed5e71e-863d-4f40-8a5f-f103a0b93ba8.png">
9. Javascript: 동적 페이지 구성
10. 웹페이지 완성


# HTML tags
* **HTML Basic**
  * &#60;html&#62; 
  * &#60;head&#62; 
  * &#60;body&#62;
* **HTML Headings**
  * &#60;h1&#62; &#60;h2&#60; ⋅⋅⋅ &#60;h6&#62;
* **HTML Paragraph**
  * &#60;p&#62; 
  * &#60;br&#62; 
  * &#60;pre&#62;
* **HTML Block**
  * &#60;div&#62; 
  * &#60;ul&#62;: Unordered List
  * &#60;ol&#62;: Ordered List
  * &#60;li&#62;: List Item
* **HTML Links**
  * &#60;a&#62;  

HTML Tutorial: <https://www.w3schools.com/html/default.asp><br/>
HTML Simulator: <https://www.w3schools.com/html/tryit.asp?filename=tryhtml_default>

# CSS Tutorials
```
p {
  color: red;
  text-align: center;
}
```
> p: Selector<br/>
> color, text-align: Property<br/>
> red, center: Value

**CSS Simple selectors**
* **element**
  * HTML elements
* **#id**
  * the id attribute of an HTML element to select a <u>specific</u> element
* **.class**
  * HTML elements with a <u>specific</u> class attribute(묶음)
* **&#42;**
  * Selects all elements
  
CSS Tutorial: <https://www.w3schools.com/css/default.asp>
