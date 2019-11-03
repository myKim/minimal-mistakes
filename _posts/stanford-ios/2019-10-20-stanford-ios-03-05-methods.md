---
title: "Methods"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

# Methods

# Parameters Names

모든 function의 파라미터에는 `internal` name과 `external` name이 있다.

- internal name은 method 내부에서 사용될 지역 변수 이름이다.
- external name은 method를 호출할 때 호출하는 사람이 사용한다.
- 함수를 호출할 때 파라미터에 external name을 사용하게 하고 싶지 않을 경우 `_`를 사용한다.
- 첫번째 파라미터에는 `_`가 기본으로 설정되어 있다.
- 다른 파라미터들은 기본값적으로 internal name이 external name이다.
- 모든 파라미터의 external name은 변경할 수 있다.
- 첫번째 파라미터에 이름을 추가하거나 나머지 파라미터에 `_`를 이용해서  이름을 지우는 것은 가능하지만, 일반적으로 이는 "anti-Swift" 표현이니 사용하지 않는 것이 좋다.

```swift
func foo(externalFirst first: Int, externalSecond second: Double) {
    var sum = 0.0
    for _ in 0..<first {
        sum += second
    }
}

func bar() {
    let result = foo(externalFirst: 123, externalSecond: 5.5)
}
```

# 오버라이드

- var나 func 앞에 `override`라는 키워드를 달면 된다.
- `final` 키워드를 앞에 붙일 경우 서브클래싱이 불가능한 메소드, 프로퍼티 혹은 클래스가 된다.
- 타입과 인스턴스 모두 메소드와 프로퍼티를 가질 수 있다.

```swift
var d: Double = ...
if d.isSignMinus {
    d = Double.abs(d)
}
```
isSignMinus는 Double 형 인스턴스의 인스턴스 프로퍼티이고
abs는 Double의 타입 메서드이다.

타입 메서드나 타입 프로퍼티를 선언할 때는 아래와 같이 앞에 `static` 키워드를 붙인다.

```swift
static func abs(d: Double) -> Double
```