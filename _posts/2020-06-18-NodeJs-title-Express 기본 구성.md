---
layout: post
title: "NodeJs: Express 기본 구성"
categories:
  - NodeJs

last_modified_at: 2020-06-18
---

Nodejs 에서 사용하는 대표적인 프레임 워크는 express가 있다. 이를 이용해 SSL 인증서를 적용해보자
우선 intellij 에서 express 환경을 세팅하면 다음과 같은 프로젝트 구성을 볼수 있다.

![디렉토리 구조](/assets/img/expressTree.PNG)

1. bin/www : 해당 프로젝트에서 서버 실행조건과 같은 설정
2. public/ : css, html과 같은 정적인 파일들
3. routes : 라우팅 관련 파일, spring 으로치면 컨트롤러 역할을 하는 파일들
4. view : 웹 에서 화면을 그릴때 보여줄 파일, 여기서는 ejs 템플릿 엔진을 사용한다.
5. app.js : 미들웨어 코드
6. package.json : 이 프로젝트에 대한 버전 정보 등