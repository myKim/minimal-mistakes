---
title: "Node.js 설치"
excerpt: "Node.js 설치"
category:
  - nodejs
tags: 
  - nodejs
---

![nodejs_logo](/assets/images/nodejs_01_install/nodejs_logo.svg)

# 설치

설치방법은 여러가지가 있다. 다양한 버전을 설치하고 스위치하며 사용하기 위해서는 **NVM(Node Version Manager)** 을 사용하는 것이 좋다.

## 직접 설치

[Node.js 공식사이트](https://nodejs.org/)에 접속해서 직접 설치한다.

 ![nodejs_install_page](/assets/images/nodejs_01_install/nodejs_install_page.png)

**LTS(Long Term Supported) 버전**은 장기적으로 안정되고 신뢰도고 높은 지원이 보장되는 버전으로, 대부분의 사용자에게 추천되는 버전이다.

**Current 버전**은 최신 기능을 제공하고 기존 API의 기능 개선에 초점이 맞춰진 버전으로, 업데이트가 잦고 기능이 변경될 가능성이 높은 버전이다.

## 패키지 매니저로 설치

여러가지 방법중 **Homebrew**를 사용해서도 설치할 수 있다.

### Homebrew로 설치

```bash
# 최신버전으로 설치된다. (Current 버전)
$ brew install node

# 8.x 버전을 설치한다.
$ brew install node@8
```

## NVM(Node Version Manager)으로 설치

### Homebrew로 NVM 설치

`brew`를 이용해서 NVM 을 설치한다.

```bash
$ brew install nvm
```

NVM 의 working directory 를 만들어준다.

```bash
$ mkdir ~/.nvm
```

`nvm` 명령어를 사용하기 위해서 `.bash_profile` 파일에 아래의 코드를 추가해준다.

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/usr/local/opt/nvm/etc/bash_completion" ] && . "/usr/local/opt/nvm/etc/bash_completion"  # This loads nvm bash_completion
```

수정한 `.bash_profile`을 적용하기 위해서 아래 명령어를 입력한다.

```bash
$ source ~/.bash_profile
```

### node 설치

아래의 명령어를 입력해서 `node`를 설치한다.

```bash
# 10.x 버전 중 최신 버전을 설치
$ nvm install 10

# LTS 버전 설치
$ nvm install --lts
```

### node 삭제

설치된 `node`를 삭제하기 위해서는 아래의 명령어를 사용한다.

```bash
# 설치된 10.x 버전을 삭제
$ nvm uninstall node 10

# LTS 버전을 삭제
$ nvm uninstall node --lts
```

### node 버전 전환

사용 버전을 전환하기 위해서 아래의 명령어를 입력한다.

```bash
# 사용 버전을 8.x 버전으로 전환
$ nvm use 8
```

### 설치된 node 버전 확인

```bash
$ nvm ls
```

# 설치 확인

설치가 정상적으로 완료되었다면 **Node.js**와 **npm(Node Package Manager)** 가 설치된다. 아래의 명령어를 입력해서 버전이 표시되면 정상설치 된 것이다. 

```bash
# Node.js 버전 확인 
$ node -v

# npm 버전 확인
$ npm -v
```

![nodejs_version_check](/assets/images/nodejs_01_install/nodejs_version_check.png)

# 참고
- https://medium.com/@moralmk/node-js-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC-%EB%B0%A9%EB%B2%95-84818ceeff08
- https://heropy.blog/2018/02/17/node-js-install/
- https://opentutorials.org/course/3332/21029
