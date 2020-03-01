---
title: "함수 포인터"
category:
  - c
tags: 
  - c
---

# 함수 포인터

C 언어에서 함수를 변수처럼 구조체나 배열에 저장하거나, 매개변수 및 반환값으로 이용한다던지 하는 것은 '함수 포인터'를 이용해서 할 수 있다. 함수 포인터는 함수를 저장하는 포인터를 뜻하고 함수 포인터를 이용해서 함수를 주고 받거나 함수를 호출할 수 있다.

## 함수 포인터 만들기

함수 포인터는 `반환값자료형 (*함수포인터이름)(매개변수)` 형태로 만든다.

```c
// 1) 매개변수가 없는 경우
void helloWorld(void) {
    printf("Hello World!");
}

// 반환값자료형 (*함수포인터이름)()
void (*fp)() = helloWorld;
void (*fp)(void) = helloWorld;

// 2) 매개변수가 있는 경우
int sum(int a, int b) {
    return a + b;
}

// 반환값자료형 (*함수포인터이름)(매개변수)
int (*fp)(int, int) = sum;
```

> 함수 포인의 형태는 objective-c의 block과 비슷하다.

## 함수 포인터 실행

함수 포인터는 일반 함수와 같이 함수포인터이름에 `()`를 붙여서 실행한다.

```c
int sum(int a, int b) {
    return a + b;
}

...

int (*fp)(int, int) = sum;
int result = fp(5, 10) // 5 + 10 = 15
```
