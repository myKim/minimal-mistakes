---
title: "상수"
excerpt: "Objective-C의 상수 정리"
category:
  - Objective-C
tags: 
  - Objective-C
  - 상수
  - Constant
---

# 상수 (Constant)

프로그램이 실행되는 내내 변하지 않는 정보를 상수(constant)라고 부른다. 오브젝티브에서는 상수를 두가지 방법으로 정의한다.

- #define
- 전역 변수(global variable)

표준 C 라이브러리에서 상수는 전처리기 지시자인 #define으로 정의된다. 그 예로 math.h 파일에 정의된 `M_PI` 는  $\pi$ 를 정의한 상수 이다.

## 전처리기 지시자

C, C++, Objective-C 의 컴파일은 두단계로 이루어진다. 우선 __전처리기(preprocessor)__ 가 전체적으로 코드를 1차적으로 처리하고, 여기서 나온 결과가 진짜 컴파일러로 들어가 컴파일이 시작된다.

전처리기 지시자는 __#__ 으로 시작되고 #include, #import, #define 등이 있다.

## #include 와 #import

기본적으로 #include 와 #import 의 역할은 같다. 전처리기에게 특정 파일을 읽어 추가하라고 하는 역할을 수행한다. 일반적으로 코드에 각종 선언들이 모인 헤더파일(.h 파일)이 포함되는데, 컴파일러는 자신이 컴파일하는 코드를 이해하기 위해서 이 파일들을 사용한다.

역할이 같은 두 지시자의 차이는 다음과 같다.

- #include 는 같은 파일을 여러번 포함하는 것을 허용한다.
- #import 는 같은 파일을 한번만 포함하라고 요청한다.

