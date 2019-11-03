---
title: "전처리기 지시자"
excerpt: "전처리기 지시자(preprocessor directives) 정리"
category:
  - C
  - Objective-C
tags: 
  - C
  - 전처리기지시자
  - preprocessor
---

[Authenticating Users with Sign in with Apple](https://developer.apple.com/documentation/signinwithapplerestapi/authenticating_users_with_sign_in_with_apple#3383773 "Authenticating Users with Sign in with Apple")




# 애플 ID 서버에서 사용자의 정보 얻기

사용가 성공적으로 인증되면, 서버는 **identity token**, **authorization code**, **user identifier**를 앱으로 리턴한다.

**identity token**은 JSON Web Token (JWT)이고 아래의 claims를 포함하고 있다.

- `iss`
  - 토큰 발급자. 값은 `https://appleid.apple.com`이다.
- `sub`
  - 사용자에 대한 고유 식별자(ID).
- `aud`
  - 당신의 Apple Developer 계정 client_id.
- `exp`
  - 토큰의 만료 시간. 이 값은 일반적으로 5분으로 설정된다.
- `iat`
  - 토큰이 발행된 시간.
- `nonce`
  - 클라이언트 세션과 ID 토큰을 연결하는데 사용되는 String 값. 이 값은 리플레이 공격(replay attack)을 완화하기 위해 사용된다. 그리고 이 값은 권한 부여 요청 중에 전달된 경우에만 존재한다.
- `email`
  - 사용자의 email 주소.
- `email_verified`
  - 이 서비스가 email을 검증했는지를 나태내는 Boolean 값이다. 이 claim의 값은 항상 true이다. 왜냐하면 서버는 오직 인증된 email 주소만 리턴하기 때문이다.

