---
title: "[Stanford iOS 강의 정리][03강] Tuple"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

# Tuple이란?

튜플은 값들의 그룹이다.
타입을 사용할 수 있는 어디에든 사용할 수 있다.

```swift
let x: (String, Int, Double) = ("hello", 5, 0.85)
// let (word, number) = x 로 할 경우 컴파일러 에러 발생
let (word, number, value) = x
print(word) // "hello"
print(number) // 5
print(value) // 0.85

// 할당 시에 element들에 이름을 정해줄 수 있다.
let x (w: String, i: Int, v:Double) = ("hello", 5, 0.85)
print(x.w) // "hello"
print(x.i) // 5
print(x.v) // 0.85

let (wrd, num, val) = x // 이름이 정해진 것도 다름이름의 변수로 할당이 가능하다.
```

# function 의 리턴값으로 사용

Tuple을 리턴값으로 사용하면 여러개의 값을 리턴값으로 보낼 수 있다.

```swift
func getSize() -> (weight: Double, height: Double) {
    return (250, 80)
}

let x = getSize()
print("weight is \(x.weight)") // weight is 250
print("height is \(getSize().height)") // height is 80
```