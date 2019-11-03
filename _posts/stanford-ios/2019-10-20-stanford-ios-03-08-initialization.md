

# Initialization

## 언제 init 메서드가 필욯할까?

`init` 메서드는 일반적이지 않다. 왜냐하면 프로퍼티들은 `=` 기호를 사용해서 그것들의 기본값을 세팅할 수 있다.
또는 프로퍼티들은 Optional이 될 수 있고, 그 경우에 nil로 세팅된다.
또한 클로저를 실행함으로써 프로퍼티를 초기화 할 수 있다.
또는 lazy instantiation을 통해서 초기화 할 수도 있다.

때문에 `init` 메서드는 오직 위의 방법들로 초기화 할 수 없을 때만 사용한다.

## 기본으로 제공되는 init 메서드도 있다.

만약 클래스의 모든 프로퍼티가 기본값을 갖는다면, 기본으로 제공되는 `init()` 메서드를 사용할 수 있다.
만약 한 구조체가 initializers를 가지고 있지 않다면, 모든 프로퍼티를 인자로 받아 초기화하는 initializer를 제공받는다.

```swift
struct MyStruct {
    var x: Int
    var y: String
}

// 자동으로 생성되는 init 메서드
let foo = MyStruct.init(x: 5, y: "hello")
```

## init 내부에서 무엇을 할 수 있을까?

- 프로퍼티의 값을 설정할 수 있다. 이미 기본값이 있는 경우에도 다시 설정이 가능하다.
- 상수 프로퍼티도 설정할 수 있다.(i.e. `let`으로 선언된 프로퍼티)
- 다른 init 메서드를 부를 수 있다.(`self.init(<args>)` 사용)
  - 여러개의 init 메소드 중 한개만 부를 수 있다.
  - 부모 클래스의 initializer를 부를 수도 있다.(`super.init(<args>)` 사용)

## init 메서드 내부의 요구사항

- init 메서드가 끝나는 시점에는 모든 프로퍼티는 반드시 값을 가져야 한다.(optional은 nil의 값을 가질 수 있다.)
- 클래스에는 convenience initializers(편의 초기화 메서드)와 designated initializers(지정 초기화 메서드) 두종류가 있다.
  - 지정 초기화 메서드는 `convenience` 단어와 함께 표시되지 않는다.
  - 편의 초기화 메서드는 `convenience init` 으로 선언한다. 
- 지정 init은 반드시(그렇게만 할 수 있다.) 부모클래스에 있는 지정 init을 호출해야 한다.
  - 지정 init은 부모 클래스의 편의 init을 호출할 수 없다.
- 부모 클래스의 init을 호출하기 전에 자식 클래스에서 만든 모든 프로퍼티들을 초기화 해야 한다.
- 부모 클래스의 어떤 프로퍼티를 건들기 전에 부모 클래스의 init을 호출해야 한다.
- 편의 init은 반드시(그렇게만 할 수 있다.) 그 클래스 안의 편의 init이나 지정 init을 호출하고 초기화해야 한다.(부모 클래스의 초기화 메서드를 호출할 수 없다.)
- 편의 init은 어떤 프로퍼티의 값을 설정할 수 있기 전에 반드시 그 init을 호출해야 한다.
- 프로퍼티에 접근하거나 메서드를 호출하려고 하기 전에 다른 init들을 부르는 것은 완료되어야 한다.
- 되도록 자기만의 init을 만드는 것을 피하자.

## init 상속

- 만약 아무런 지정 init도 실행하지 않는다면, 모든 부모클래스의 지정 init들이 상속된다.
- 만약 부모클래스의 모든 init을 오버라이드 한다면, 부모클래스의 모든 편의 init들이 상속된다.
- 만약 아무런 init도 실행하지 않는다면, 부모클래스의 모든 init들이 상속된다.
- 상속된 모든 init들은 위의 init의 요구사항을 따른다.

## required 키워드

- `required` 키워드와 init을 함께 표기할 수 있다.
- 자식클래스에서 반드시 이 init을 실행해야 한다는 뜻이다.

## 실패할 수 있는 init

init이 ?(또는 !)를 뒤에 가지고 선언된다면, 이것은 Optional 값을 리턴한다.

```swift
init?(arg1: type1, ...) {
    // nil이 리턴될 수 있다.
}

let image = UIImage(named: "foo") // image는 Optional UIImage이다.(i.e. UIImage?)
// 이런 경우 일반적으로 if-let 구문을 사용한다.
if let image = UIImage(named: "foo") {
    // 이미지 생성 성공
}
else {
    // 이미지 생성 실패
}
```