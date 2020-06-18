---
layout: post
title: "NodeJs: dotenv 설치"
categories:
  - NodeJs

last_modified_at: 2020-06-18
---

개발을 하다보면 반드시 각 배포환경에 맞게 설정들을 분기해야 될 경우가 생긴다(배포, 개발, 로컬, 기타 ..)
예를 들어 Spring 의 경우 Vm args를 받아서 해당 변수로 분기를 해 배포환경을 구분할 수 있다.

NodeJs의 경우는 해당 서비스가 배포되는 로컬환경의 환경변수에 접근하여 분기가 가능한데
이를 좀 더 쉽게 도와줄 dotenv라는 플러그인을 설치 해보자

## 설치
1. npm install dotenv
2. 프로젝트 최상단에 .env 파일 생성

끝(~~~쉽다~~~)

## .env 파일 설정
````..env
#프로젝트 환경
NODE_ENV = production
````
spring 의 properties 사용법과 상당히 유사하다 key-value 형태로 사용하면 된다.


## 실 사용
```javascript
require('dotenv').config();
console.log("ENV OPT : "+process.env.NODE_ENV);
```
1. require('dotenv').config()
 - env 파일 설정을 가져온다.
2. console.log("ENV OPT : "+process.env.NODE_ENV)
 - process.env로 접근해서 .env 파일에서 선언한 NODE_ENV 변수의 값을 가져온다.
 
끝(~~~쉽다2~~~)

기본적으로 이렇게 각 배포환경에 맞게 분기를 탈수 있는 env 파일을 만들어 두고 필요시 분기해서 개발을 하면된다.
단, env 파일은 각 배포환경마다 다를것이기 때문에 변경하지 않도록 해야한다 처음에 파일을 생성해놓고 git ingnore에 추가하는것도 좋은 방법인것 같다.
다음엔 SSL 인증서 적용하는걸 해보자