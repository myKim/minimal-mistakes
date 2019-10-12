---
title: "URL이란?"
category:
  - URL
  - web
tags: 
  - URL
  - web
---

# URL이란?

URL(Uniform Resource Locator)은 인터넷에서 자원의 위치를 나타낸다.

# URL의 구조

아래의 example URL을 통해 구조를 확인해보자.

```
http://www.example.com/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument
```

## Protocol

`http` 는 프로토콜(규약)이다. 이는 브라우저가 어떤 규약을 사용해야 하는 지를 나타낸다. 프로토콜은 컴퓨터 네트워크에서 데이터를 교환하거나 전송하기 위한 방법들의 세트이며 HTTP 외에도 FTP 등의 프로토콜 등이 존재한다.

## Domain(Host) Name

`www.example.com` 은 도메인(또는 호스트) 이름이다. 이것은 웹 서버의 주소를 의미한다. 직접 IP 주소를 사용하는 것도 가능하다.

## Port

`:80` 은 포트이다. 포트는 웹서버에서 자원을 접근하기 위해 사용하는 "관문(gate)" 번호를 나타낸다. 표준 HTTP 포트(HTTP는 80, HTTPS는 443)의 경우 포트 번호는 생략이 가능하다. 그렇지 않을 경우에 포트 번호는 필수이다.

## Path

`/path/to/myfile.html` 은 웹서버에서 자원에 대한 경로이다. 초기의 웹에서는 웹서버상에서의 물리적 파일 위치를 나타냈지만, 요즘에는 실제 물리적 경로를 나타내지 않고 웹 서버에서 추상화된 경로를 나타낸다.

## Query String(Parameters)

`?key1=value1&key2=value2` 는 웹서버에 전송하는 추가 파라미터이다. 쿼리 스트링은 `?` 기호로 시작하고 `&` 기호로 구분된 Key/Value 리스트이다. 웹서버는 사용자가 자원 요청 시에 해당 값을 전달 받는다. 그리고 이 파라미터 값을 내부적인 작업을 위해 사용할 수 있다.

## Anchor

`#SomewhereInTheDocument` 는 단어 그대로 자원 자체의 다른 부분에 대한 anchor(닻)이다.

anchor는 문서에서 일종의 bookmark라고 할 수 있다. 브라우저가 bookmark된 지점의 내용을 보여주게 하기 위해서 해당 지점을 알려주는 역할을 한다.

예를 들어 HTML 문서에서 anchor는 브라우저에게 bookmark된 지점을 알려주고 브라우저는 anchor 지점으로 스크롤해 해당 부분을 사용자에게 보여준다.

anchor는 HTML 문서에 국한된 것이 아니라 비디오나 오디오 문서 등에서도 작동한다. 비디오나 오디오 문서에서 anchor를 지정하면 브라우저는 anchor가 나타내는 시간을 찾으려고 한다.

유튜브 예시
https://www.youtube.com/watch?v=UM8_pjQa9pw#t=2m00s

`#` 뒤에 오는 부분은 브라우저에서 사용할 뿐, 실제로 요청이 서버에 보내지지 않는다.

# 참고

- https://developer.mozilla.org/ko/docs/Learn/Common_questions/What_is_a_URL
