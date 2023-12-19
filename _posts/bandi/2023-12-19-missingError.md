---
layout: single
title: \[Error] Missing purpose string in Info.plist & Missing Push Notification Entitlement
toc: true
toc_sticky: true
categories: [iOS distribute]
---

## 굉장히 많은 도움을 받았다.
<img width="268" alt="image" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/d26d7f94-0922-48f4-92fc-88bcc255ba61">     
\[코딩파파] Flutter iOS 앱 배포 2023 | 애플 앱 스토어 : <https://www.youtube.com/watch?v=i9B7xd48QTY>

## 출시 전 에러 발견!
<img width="1022" alt="image" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/037de823-77a7-4773-b201-0a882d77ce1b">
> App Store Connect로 넘겨주기 위해 *Validate App* 이후 *Distribute App* 시도!

## 하지만 아무리 기다려도 빌드가 뜨지 않았다!!
<img width="979" alt="image" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/d93eb0bc-b6f0-49d2-94a2-642f3abef7a0">
> 영상에서는 30분을 기다려보라는데.. 2시간이 넘게 기다렸다...

## 이메일을 확인해보자!
<img width="1086" alt="image" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/c86f3568-01d3-411c-a24d-d99c52559708">
> 혹시나 해서 들어간 이메일에 연락이 와 있었다..    
*<span style="color: red">ITMS-90683: Missing purpose string in Info.plist</span>*     
*<span style="color: red">ITMS-90078: Missing Push Notification Entitlement</span>*      
> 이 링크를 통해 에러를 해결할 수 있었다! -> [https://velog.io/@bargoloft/TMS-90683-Missing-Purpose-String-in-Info.plist-ITMS-90078-Missing-Push-Notification-Entitlement-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0]

## Missing purpose string in Info.plist
Info.plist에 필요한 태그에 대한 목적이 필요하다고 한다!     
iOS/Runner/Info.plist 파일에 다음 코드를 추가한다.
```
<dict>
    <key>NSMicrophoneUsageDescription</key> 
    <string>to convert voice to text</string>
```
> \<key> 태그 안 필드는 메일에서 알려준 문제가 되는 필드를 입력해야 한다.

## Missing Push Notification Entitlement
Push Notification을 사용할 경우 이 과정이 필요하다       
간단하게 Xcode > Targets > Runner > Signing & Capabilities > Capability > Push Notification 추가     
<https://mdpapa.tistory.com/143>

## 후.. 드디어 빌드 완료
해결이 되었다면 10분 안에 다시 메일이 온다!
<img width="739" alt="291512790-4f444c98-23eb-432c-9fd0-2794455e122e" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/14819695-dfd1-4fff-80aa-2ac8745e7500">


<img width="1163" alt="image" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/a7634fc1-b7ed-4961-af2b-6fff2f503b0e">
빌드 완료 후 다시 영상을 따라 가보자!
