---
layout: single
title: "[HTML5&CSS3] Content 상관없이 aside, footer 고정시키기"
toc: true
toc_sticky: true
categories: htmlcss
published: true
---


`<aside>`, `<footer>` 고정 시키기

- `position: fixed`
- aside의 경우 `right: 0` 로 고정, `bottom: ?px` 으로 띄우기
- footer의 경우 `bottom: 0` 으로 고정

## 코드

```css
aside {
    position: fixed;
    right: 0; 
    bottom: 500px;
    z-index: 1000;
}

footer {
    background-color: #f1f1f1;
    text-align: center;
    position: fixed;
    width: 100%;
    bottom: 0;
}
```
> Github: <https://github.com/KimGyeongLock/resume>

## 문제 상황
![998ef591-2eb4-49ba-a86f-031eb38082d9](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/3a7a0b6b-7460-4bc6-a3f9-2a90f277f96f)


> 왜 제 위치로 가지 않는가??
> 

⇒ 제 위치로 간 것이다.

<img width="801" alt="Untitled" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/29bebd7b-13c7-498b-a017-29155b26f2e8">


- Contents의 길이가 짧기 때문에 페이지가 짧아진거지 제 위치에 있다.

![5185740f-23fe-42c3-bf23-48f5d7069670](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/7cefa8ba-c1b5-460a-b025-7afbc816f987)


- Content에 상관없이 **고정**시키려면 어떻게 해야할까??

⇒ `CSS` 를 사용해야 한다!!

![Untitled 1](https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/a434f6e0-9941-4543-9a2e-1ad0923a23a4)

## 추가 HTML5, CSS3 공부

### HTML에 외부 CSS 적용법

`<head>` 안에 아래 코드를 넣는다.

```html
 <link rel="stylesheet" href="style.css">
```

### Flexbox 또는 Grid로 섹션 위치 크기 조정
```css
.edu-item {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
.profile {
    flex: 1;
    ...
}
.info {
    flex: 1.3;
    ...
}
```
> 공부: <https://tlsdnjs12.tistory.com/4>
