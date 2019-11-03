---
title: "[Stanford iOS 강의 정리][03강] AnyObject"
category:
  - iOS
  - swift
tags: 
  - iOS
  - swift
---

# AnyObject

`AnyObject`는 특별한 타입이다.(실제로는 protocol 이다.)

일반적으로 Objective-C API들과 호환하기 위해 사용되곤 했다.
하지만 iOS9 이후로 Objective-C API들이 업데이트 되어 더 이상 그렇게 사용하지 않는다.
Objective-C에서 `id`는 모르는 클래스의 객체에 대한 포인터 주소를 말한다.
AnyObject는 id를 호환하기 위해 나온 것이다.
클래스에 대한 객체에만 사용하고 구조체나 enum에는 사용하지 않는다.

Swift에 다른 타입으로 `Any`도 있다. Any는 말그대로 어떤 것이든 될 수 있다.(매우, 매우 드물게 사용된다.)

## AnyObject가 언제 사용될까?

메서드 인자의 타입이 적어도 두개 이상 될 수 있을 때

```swift
// 화면 전환할 때 호출되는 메서드
// sender가 버튼일지, 테이블의 row일지 알 수 없기 때문에 AnyObject를 쓴다.
func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject)
```

또는 cookie를 반환하려고 할 때
객체를 호출자가 무엇인지 알지못하게 하고 싶을 때

## 어떻게 AnyObject 타입의 변수를 사용할까?

AnyObject를 사용하기 위해서는 반드시 다른 알고있는 class(또는 protocol)로 변환해 주어야 한다.

변환이 가능하지 않을 수도 있다. 때문에 변환은 Optional 객체를 생성한다.
변환은 `as?` 키워드를 통해 이루어진다.(또는 `as!` 를 사용하고 이는 강제적으로 Optional을 해제한다.)

일반적으로 `as?`는 `if let`구문과 같이 사용한다.

```swift
let ao: Anyobject = ...
if let foo = ao as? SomeClass {
    // 변환이 성공할 경우 foo 객체를 SomeClass 타입으로서 사용할 수 있다.
}
```


# Plist






# NSUserDefault