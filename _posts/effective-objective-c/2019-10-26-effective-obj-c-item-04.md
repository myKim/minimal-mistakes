---
title: "[Effective Objective-C 정리][아이템 04] 전처리기 #define보다는 타입이 있는 상수를 사용하라"
category:
  - objective-c
tags: 
  - objective-c
---

# 아이템 4: 전처리기 #define보다는 타입이 있는 상수를 사용하라

코드를 작성 중 상수를 정의하고 싶을 때 전처리기 지시어 `#define`을 이용한 방법을 많이 사용한다.


```objc
#define ANIMATION_DURATION 0.3
```

## \#define 사용의 문제점

- 타입에 대한 정보가 없다.
- 이름을 'DURATION'으로 선언한 것으로 의미를 유추할 수 있지만 명확하지 않다.
- 헤더 파일에 선언되어 있다면 그 헤더 파일을 포함하는 모든 곳의 `ANIMATION_DURATION`이 값으로 치환되며 작동한다.

상수를 정의할 때 전처리기 지시자를 사용하는 것보다 상수를 정의하는 것이 더 좋은 방법이다.

```objc
static const NSTimeInterval kAnimationDuration = 0.3;
```

## 상수 정의의 장점

- 타입이 명확하기 때문에 상수가 무엇을 하는지 더 정확하게 정의한다.
- 명확한 타입 정보는 그 자체로 문서 역할을 한다.

> - 내부적으로 변환 단위를 표현하는 상수의 일반적인 표기법은 k 소문자를 상수 맨 앞에 붙이는 것이다.
> - 클래스 외부로 노출되는 상수는 일반적으로 클래스 이름을 상수 앞에 붙여준다. (아이템 19 확인)

## 상수 사용 주의점

Objective-C는 네임스페이스(namespace)라는 개념이 없기 때문에 kAnimationDuration이라는 전역 변수로 정의된다. 때문에 이 이름은 EOCViewClassAnimationDuration처럼 사용될 범위를 나타내는 접두어를 반드시 붙여야 한다. (자세한 명명법은 아이템 19 확인)

외부로 노출할 필요가 없는 상수는 사용되는 구현 파일(.m)에 정의해야 한다.

상수를 정의할 때 `static`, `const` 둘 다 사용해야 한다. `const`는 값의 변경을 허용하지 않는 것을 의미하고, `static`은 변수가 정의된 번역 단위(translation unit, 소스 파일에서 C 전처리가 끝난 파일)의 지역 변수라는 것을 의미한다.
컴파일러는 최종적으로 번역 단위를 입력으로 받아 목적 파일(object file)을 만든다. Objective-C에서 모든 구현파일(.m)당 한 개의 번역 단위가 있다. 
`static`으로 선언되면 그 상수는 선언된 파일(.m)로부터 생성된 목적 파일에 지역적으로 선언된다.
`static`으로 선언되지 않으면 컴파일러는 그것을 위해 외부 심벌(external symbol)을 생성한다.
다른 번역 단위에 같은 이름의 변수를 선언하면 링커는 duplicate symbol 에러를 일으킨다.

아래와 같이 `static`을 사용하지 않고 ClassA와 ClassB에 kAnimationDuration을 선언해보자.

```objc
// ClassA.m
#import "ClassA.h"

const NSTimeInterval kAnimationDuration = 0.3;

@implementation ClassA
...
@end

// ClassB.m
#import "ClassB.h"

const NSTimeInterval kAnimationDuration = 0.5;

@implementation ClassB
...
@end
```

컴파일 시 아래와 같은 에러가 발생한다.

```
duplicate symbol '_kAnimationDuration' in:
    /.../ClassB.o
    /.../ClassA.o
```

`static`과 `const`를 모두 사용하면 컴파일러는 절대 심벌을 만들지 않는다. 대신 `#define`으로 정의했을 때처럼 사용된 모든 변수를 값으로 치환한다. 하지만 타입 정보 제공의 이점이 있다.
