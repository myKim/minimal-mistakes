---
title: "[Stanford iOS 강의 정리][03강] Range"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

# Range란?

Swift에서 Range는 두개의 끝점이다.
Range는 제네릭이다. (e.g. Range<T>)

```swift
let array = ["a", "b", "c", "d"]
let subArray1 = array[2...3] // subArray1 = ["c", "d"]
let subArray2 = array[2..<3] // subArray2 = ["c"]
for i in 27...104 {
    // process
}
```