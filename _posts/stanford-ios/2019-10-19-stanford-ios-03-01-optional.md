---
title: "Optional"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

# Optional

Optional은 enum 이다.
두가지 case를 가진 enum 으로 set 되지 않은 `None` case와 set된 `Some` case가 있다.

```swift
enum Optional<T> {
    case None
    case Some(T)
}
```

```swift
let x: String? = nil
// 위 구문은 아래와 같다.
let x = Optional<String>.None

let x: String? = "hello"
// 위 구문은 아래와 같다.
let x = Optional<String>.Some("hello")


// 추출
var y = x!
// 위 구문은 아래와 같다.
switch x {
    case Some(let value): y = value
    case None: // raise an exception
}

let x: String? = ...
if let y = x {
    // do someting with y
}
// 아래와 같다.
switch x {
    case .Some(let y):
        // do something with y
    case .None:
        break
}
```

## Optional Chaining

Optional들은 연결될(chained) 수 있다.

```swift
var display: UILabel?
if let label = dispaly {
    if let text = label.text {
        let x = text.hashValue
        ...
    }
}
// ... or ...
if let x = display?.text?.hashValue {
    ...
}
```

위의 let x는 무슨 타입일까? 타입 추출이 실패해서 nil을 가질 수 있기 때문에 Optional이 되어야 하고, hashValue가 Int이기 때문에 Optional<Int>가 된다.


## ?? 연산자

nil 일 때의 기본값을 제공한다.

```swift
let s: String? = ... // might be nil
if s != nil {
    display.text = s
}
else {
    display.text = " "
}
// 간단한 방법
display.text = s ?? " "
```