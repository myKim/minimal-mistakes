---
title: "Task 한번만 실행"
category:
  - objective-c
tags: 
  - objective-c
---

# 토큰

## dispatch_once_t

`dispatch_once`, `dispatch_once_f` 에서 사용되는 단 한번 실행을 확인하기 위한 predicate

> 참고 : [dispatch_once_t](https://developer.apple.com/documentation/dispatch/dispatch_once_t?language=objc)

### 선언

```objc
typedef intptr_t dispatch_once_t;
```

### 설명

이 타입의 변수들은 반드시 global 또는 static 범위에 있어야 한다.

# 함수

## dispatch_once

App에서 정의된 block을 App의 Lifetime 동안 단 한번만 실행한다.

> 참고 : [dispatch_once](https://developer.apple.com/documentation/dispatch/1447169-dispatch_once?language=objc)

### 선언

```objc
void dispatch_once(dispatch_once_t *predicate, dispatch_block_t block);
```

### 파라미터

- **predicate**
  - 해당 block이 처리완료 되었는지 아닌지를 확인하는데 사용되는 `dispatch_once_t` 구조체에 대한 포인터
- **block**
  - 단 한번 실행할 block 객체

### 설명

다중 스레드에서 동시에 호출된다면, 이 함수는 작업중인 함수가 완료 될 때까지 동기적으로 대기한다.

`predicate`는 반드시 **global** 또는 **static** 범위에 변수의 포인터이어야 한다. 다시 말해서 Object-C 의 인스턴스 변수와 같은 **automatic** 또는 **dynamic** 공간의 변수를 사용하면 안된다.

## dispatch_once_f

App에서 정의된 함수를 App의 Lifetime 동안 단 한번만 실행한다.

> 참고 : [dispatch_once_f](https://developer.apple.com/documentation/dispatch/1447167-dispatch_once_f?language=objc)

### 선언

```objc
void dispatch_once_f(dispatch_once_t) *predicate, void *context, dispatch_function_t function);
```

### 파라미터

- **predicate**
  - 해당 함수가 처리완료 되었는지 아닌지를 확인하는데 사용되는 `dispatch_once_t` 구조체에 대한 포인터
- **context**
  - 실행할 함수로 전달할 context 파라미터
- **function**
  - 단 한번 실행할 App에서 정의된 함수, 이 함수로 전달되는 파라미터는 `context` 파라미터이다. 이 파라미터는 NULL이 될 수 없다.

### 설명

다중 스레드에서 동시에 호출된다면, 이 함수는 작업중인 함수가 완료 될 때까지 동기적으로 대기한다.

`predicate`는 반드시 **global** 또는 **static** 범위에 변수의 포인터이어야 한다. 다시 말해서 Object-C 의 인스턴스 변수와 같은 **automatic** 또는 **dynamic** 공간의 변수를 사용하면 안된다.
