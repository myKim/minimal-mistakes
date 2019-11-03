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

# 전처리기 지시자(Preprocessor Directives)

C, C++, Objective-C 의 컴파일은 두 단계로 이루어진다. 우선 __전처리기(preprocessor)__ 가 소스코드를 1차적으로 처리하고, 여기서 나온 결과로 컴파일러가 컴파일을 수행한다.

__전처리기 지시자(preprocessor directives)__ 는 전처리기가 처리해야 할 일을 가르쳐주는 문장이라고 할 수 있다.

 전처리기 지시자는 __#__ 으로 시작되고 #include, #import, #define 등이 있다.

C 계통의 언어의 문장은 세미콜론(;)으로 끝나지만 
전처리기 지시자는 세미콜론으로 끝나지 않는다.

# 전처리기 지시자의 종류

## \#include

헤더파일(.h)과 같은 외부 파일을 포함시키려고 할 때 사용한다.

```objc
#include <stdio.h>      // stdio.h 파일을 포함시킨다.
#include "TestHeader.h" // TestHeader.h 파일을 포함시킨다.
```

대상 파일을 지칭할 때 __<>__(홑화살괄호)를 사용하거나 __""__(큰따옴표)를 사용할 수 있다. __<>__ 와 __""__ 의 차이점은 __<>__ 는 파일을 찾을 때 컴파일러의 표준 라이브러리 폴더부터 검색하는 것을 기본으로 한다. 그리고 __""__ 는 현재 디렉토리 부터 검색하는 것을 기본으로 한다.

> __\#include \<파일명\>__
> - 파일을 찾을 때 표준 라이브러리 폴더부터 검색
> - 일반적으로 표준 라이브러리를 사용할 때 사용
> 
> __\#include "파일명"__
> - 파일을 찾을 때 현재 디렉토리부터 검색
> - 일반적으로 사용자 작성 라이브러리를 사용할 때 사용

## \#define

__\#Define__ 은 식별자와 토큰 문자열을 연결 하는 _매크로_ 를 만든다. 매크로가 정의되면 소스코드 내의 식별자는 토큰 문자열로 치환된다.

```c
// #define 식별자 토큰문자열
#define MAX_VALUE   100

// #define 식별자(식별자, ... , 식별자) 토큰문자열
#define SUM(a, b) (a + b)
```

첫 번째 경우처럼 상수를 정의하기 위해 사용되기도 하고, 두 번째의 경우처럼 함수와 같이 사용되기도 한다. `SUM(1, 2)`를 호출하면 `(1+2)`로 코드가 치환되는 것이다.

토큰문자열은 __소스코드 그 자체__ 로 치환되기 때문에 자료형에 구애받지 않고 사용할 수 있다.

```c
#define NAME "Mike"

// 위와 같이 NAME 을 정의하고 사용하면
printf(NAME);

// 전처리기에 의해 아래와 같이 치환된다.
printf("Mike");
```

\#define 으로 정의된 상수를 사용할 경우와 일반적 변수를 사용할 경우 차이가 있다.

```c
#define NAME "Mike"     // 전처리기 지시자를 사용한 상수
char my_name[] = "Mike" // char 배열 변수
```

위와 같이 정의와 변수 선언을 하고 사용을 해보자.

```c
printf(NAME);
printf(NAME);
printf(my_name);
printf(my_name);
```

위의 코드는 아래와 같이 치환될 것이다.

```c
printf("Mike");
printf("Mike");
printf(my_name);
printf(my_name);
```

이 결과에서 확인할 수 있는 점은 변수는 하나의 동일한 문자열을 두번 사용한 반면, 전처리기 명령어를 사용했을 경우에는 두개의 문자열을 사용한다는 것을 알 수 있다. 이런 경우 메모리 낭비를 가져온다는 것을 알 수 있다.

## \#undef

\#define 으로 정의되어 있는 매크로를 무효화한다.

```c
#define SUM(a, b) (a + b)

#undef SUM(a, b)
```

라고 할 경우 컴파일 시 `Undefined symbol: _SUM` 에러가 발생하는 것을 확인할 수 있다.

## \#if ~ \#endif

if 구문과 동일한 조건문이다. 이런 조건문들을 이용해서 조건에 따라 구문을 컴파일할지 안할지를 정해줄 수 있다.

```c
#define A 1
#if A
    source code 
#endif
```

위와 같이 작성할 경우 A 가 0 이 아니기 때문에 source code 부분은 컴파일 된다.

```c
#define B 0
#if B
    source code 
#endif
```

반면에 이 경우에는 B 가 0 으로 C언어에서의 false 값이기 때문에 source code 부문은 컴파일 되지 않는다.

## #ifdef ~ \#endif


## #ifndef ~ \#endif


## \#if defined


## \#error


## \#line


# 참고 : C의 predefined macro



# 참고문서

https://docs.microsoft.com/ko-kr/cpp/preprocessor/hash-define-directive-c-cpp?view=vs-2019

http://sarghis.com/blog/802/
