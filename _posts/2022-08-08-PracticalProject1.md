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
 * 변경 전<br/>
   <img width="384" alt="스크린샷 2022-08-08 오후 2 54 20" src="https://user-images.githubusercontent.com/63464299/183356859-36dc8b12-74a5-433e-b2d5-abc28fe1b6f8.png">
 * 변경 후<br/>
  <img width="384" alt="스크린샷 2022-08-08 오후 2 52 36" src="https://user-images.githubusercontent.com/63464299/183352476-9ed5e71e-863d-4f40-8a5f-f103a0b93ba8.png">
9. Javascript: 동적 페이지 구성
10. 웹페이지 완성


# HTML tags
* **HTML Basic**
  * &#60;html&#62;: HTML document's Start and End
  * &#60;head&#62;: 해당 문서에 대한 정보인 메타데이터(metadata)의 집합을 정의
    - &#60;title&#62;
    - &#60;style&#62;
    - &#60;base&#62;
    - &#60;link&#62;
    - &#60;meta&#62;
    - &#60;script&#62;
    - &#60;noscript&#62;
  * &#60;body&#62;: The visible part of the HTML document
  ```
  <!DOCTYPE html>
  <html>
  <head>
  <title>Page Title</title>
  </head>
  <body>

  <h1>This is a Heading</h1>
  <p>This is a paragraph.</p>

  </body>
  </html>
  ```
* **HTML Headings**
  * &#60;h1&#62; &#60;h2&#60; ⋅⋅⋅ &#60;h6&#62;
  * &#60;h1&#62; defines the most important heading. 
  * &#60;h6&#62; defines the least important heading: 
  ```
  <h1>Heading 1</h1>
  <h2>Heading 2</h2>
  <h3>Heading 3</h3>
  <h4>Heading 4</h4>
  <h5>Heading 5</h5>
  <h6>Heading 6</h6>
  ```
* **HTML Paragraph**
  * &#60;p&#62;: Paragraph
  ```
  <p>This is a paragraph.</p>
  <p>This is another paragraph.</p>
  ```
  * &#60;br&#62;: Line Break
  ```
  <p>This is<br>a paragraph<br>with line breaks.</p>
  ```
  * &#60;pre&#62;: Preformatted Text
  ```
  <pre>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
  </pre>
  ```
* **HTML Block**
  * &#60;div&#62;: Division or Section
  ```
  <div>Hello World</div>
  ```
  * &#60;ul&#62;: Unordered List
  ```
  <ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
  </ul>
  ```
  * &#60;ol&#62;: Ordered List
  ```
  <ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
  </ol>
  ```
  * &#60;li&#62;: List Item
* **HTML Links**
  * &#60;a&#62;: Hyperlink
  ```
  <a href="url">link text</a>
  ```

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
