---
title: "[Stanford iOS 강의 정리][03강] Properties"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

Swift에서 `willSet`과 `didSet`을 통해 프로퍼티의 변화를 observe할 수 있다.

```swift
// 저장 프로퍼티
var someStoredProperty: Int = 42 {
    willSet { newValue is the new value }
    didSet { oldValue is the old value }
}

// 상속된 프로퍼티
override var inheritedProperty {
    willSet { newValue is the new value }
    didSet { oldValue is the old value }
}

// Type 값이 변경되어도 호출된다. (참조타입은 해당되지 않는다.)
var operations: Dictionary<String, Operation> = [ ... ] {
    willSet { will be executed if an operation is added/removed }
    didSet { will be executed if an operation is added/removed }
}
```

didSet과 willSet이 가장 많이 사용되는 것은 UI를 업데이트 하는 것이다.

# Lazy Initialization

lazy property는 누군가가 이것에 접근할 때까지 초기화되지 않는다.

```swift
// 해당 시점에 초기화 되지 않고, brain을 사용하는 시점에 초기화된다.
lazy var brain = CalculatorBrain() // CalculatorBrain이 많은 리소스를 사용한다면 좋다.
```

var만 사용할 수 있다.