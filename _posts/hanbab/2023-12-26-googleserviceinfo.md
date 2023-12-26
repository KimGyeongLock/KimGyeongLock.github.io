---
layout: single
title: \[Error] Please register custom URL scheme 'com.googleusercontent.apps... (iOS)
toc: true
toc_sticky: true
categories: [phone auth]
---

iOS에서는 되는 firebase SMS 인증방식이 안드로이드에서 말썽이다..    
```
E/FirebaseAuth(31454): [SmsRetrieverHelper] SMS verification code request failed: unknown status code: 17020 null
D/FirebaseAuth(31454): Invoking original failure callbacks after phone verification failure for +82 10-0000-0000, error - A network error (such as timeout, interrupted connection or unreachable host) has occurred.
I/flutter (31454): Phone number verification failed. Code network-request-failed. Message A network error (such as timeout, interrupted connection or unreachable host) has occurred.
```
아무리 해도 안되길래 클론 코딩 하나 생성하여 다시 해보는 중이다.   
이 에러도 나중에 올릴 예정이다.

## SMS 인증 iOS 에서 빼먹지 말아야 할것!
```
flutter: Phone number verification failed. Code unknown.
Message Please register custom URL scheme 'app-1-216730966705-ios-62d640c4e1dc0d224fa090' in the app's Info.plist file.
```
1. GoogleService-Info.plist 파일에서 REVERSED_CLIENT_ID 키를 찾아 복사
2. xcode -> TARGETS -> Info-> URL Type -> URL Schemes에 REVERSED_CLIENT_ID를 붙여넣기
<img width="652" alt="스크린샷 2023-12-26 오후 10 18 19" src="https://github.com/KimGyeongLock/KimGyeongLock.github.io/assets/63464299/43d1d411-b486-41a7-ba01-6dd1e9aa596a">

<https://velog.io/@dormahd114/firebase-%EC%A0%84%ED%99%94-%EC%9D%B8%EC%A6%9DIOS%EC%8B%9C-Please-register-custom-URL-scheme-com.googleusercontent.apps...-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0>

## GoogleService-Info.plist 주의 사항
REVERSED_CLIENT_ID 키가 필드에 없다면?   
**<span style="color: red">Google Sign In 등록 후 GoogleService-Info.plist를 다시 다운 받는다면 생길 것이다!!</span>**
<https://stackoverflow.com/questions/77220339/client-id-reversed-client-id-and-android-client-id-missing-from-googleservice-i>
