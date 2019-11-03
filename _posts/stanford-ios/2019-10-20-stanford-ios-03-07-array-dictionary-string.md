

# Array

```swift
// 정식 표현
var a = Array<String>()
// 약식 표현
var a = [String]()

let animals = ["Giraffe", "Cow", "Doggie", "Bird"]
animals.append("Ostrich") // animals가 let으로 선언되어 immutable이기 때문에 컴파일되지 않는다. (var로 선언시 컴파일된다.)

let animal = animals[5] // array index out of bounds 크래시 발생

// enumerating an Array
for animal in animals {
    println("\(animal)")
}
```


```swift
// filter
// 원하지 않는 element들이 걸러진 새로운 배열을 만든다.
// Array의 각각의 요소마다 클로저를 실행하고, 클로저가 true를 반환하는 요소들을 포함해 나간다.
filter(includeElement: (T) -> Bool) -> [T]
let bigNumbers = [2,47,118,5,9].filter({ $0 > 20 })

// map
// Array 안에 있는 각 요소들을 다른 것으로 바꾼 새 배열을 만든다.
// 변환되는 것들은 Array 안에 있는 것과 다른 타입으로 바뀔 수 있다.
map(transform: (T) -> U) -> [U]
let stringified: [String] = [1,2,3].map { String($0) }

// reduce
// 전체의 Array를 하나의 결과로 줄인다.
reduce(initial: U, combine: (U, T) -> U) -> U
let sum: Int = [1,2,3].reduce(0) { $0 + $1 } // 0부터 시작해서 각 element들을 더한다.
```

```swift
// 트레일링 클로져 문법 (trailing closure syntax)
// 클로저가 함수의 마지막 인자이면 클로저를 함수의 소괄호 바깥에 둘 수 있다.
let stringified: [String] = [1,2,3].map({ String($0) })
let stringified: [String] = [1,2,3].map { String($0) } // 트레일링 클로져 문법

let sum: Int = [1,2,3].reduce(0, { $0 + $1 })
let sum: Int = [1,2,3].reduce(0) { $0 + $1 } // 트레일링 클로져 문법
```


# Dictionary

```swift
// 정식 표현
var pac10teamRankings = Dictionary<String, Int>()\
// 약식 표현
var pac10teamRankings = [String:Int]()

pac10teamRankings = ["Stanford":1, "Cal":10]
let ranking = pac10teamRankings["Ohio State"] // ranking의 자료형은 Int? 이다. (값은 nil)

// Dictionary를 열거(enumerate)하기 위해서 tuple을 이용한다.
for (key, value) in pac10teamRankings {
    print("\(key) = \(value)")
}

// 사용하지 않을 부분에는 '_'(언더바)를 쓰면 된다.
for (key, _) in pac10teamRankings {
    print("\(key)")
}
```


# String

Swift에서 String은 전부 유니코드이다.

String은 자동으로 Objective-C의 클래스인 NSString과 연결된다. 그래서 몇가지 호출할 수 있는 메소드는 String의 문서에 존재하지 않는다. 대신에 NSString의 문서에서 해당 메소드를 찾을 수 있다.

```swift
startIndex -> String.Index
endInedx -> String.Index
hasPrefix(String) -> Bool
hasSuffix(String) -> Bool
capitalizedString -> String
lowercaseString -> String
uppercaseString -> String
components(separatedBy: String) -> [String]
// "1,2,3".components(separatedBy: ",") = ["1", "2", "3"]
```



# Other Classes

## NSObject

NSObject는 모든 Objective-C 클래스의 기본 클래스다.
Swift에서는 클래스는 의무적으로 기본 클래스를 상속하지 않아도 된다. 하지만 모든 Objective-C 클래스는 NSObject의 자식 클래스가 되어야 한다.

Swift에서 몇가지 경우를 제외하고는 NSObject를 상속하든 상속하지 않든 아무런 문제가 없다.

## NSNumber

Swift에서 Array, Dictionary, Double, Int는 모두 구조체이다.
Objective-C에서 Array, Dictionary는 클래스, Double, Int는 C의 double과 int이다.(객체가 아니다.) 이는 몇가지 문제를 가져오는데, 한가지는 Array에 숫자를 넣으려고 한다면 double과 int가 primitive 타입이기 때문에 객체인 Array에 값을 넣을 수 없다.
때문에 NSNumber로 primitive 타입인 int와 double을 랩핑해서 Array에 넣는다.

Swift에서는 Int, Double이 구조체이기 때문에 따로 랩핑 없이 Array에 값을 넣을 수 있다. 때문에 NSNumber가 불필요하다.

```swift
let n = NSNumber(35.5)
let intversion: Int = n.intValue // doubleValue, boolValue, etc.
```


## NSDate

UI에 날짜를 보여주고 싶을 때, 자동으로 지역화되는 NSDate를 사용하자.
NSCalendar, NSDateFormatter, NSDateComponents도 같이 확인해보자.

## NSData

NSData는 비트데이터의 모음(bag o' bits)이다.
iOS SDK를 통해 raw 데이터를 저장/복원/전송할 때 사용한다.
