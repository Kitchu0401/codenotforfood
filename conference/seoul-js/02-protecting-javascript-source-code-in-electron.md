# Protecting javascript source code in Electron by @2woongjae

메인 프로세스와 랜더러 프로세스로 분리
- 메인 프로세스: 노드와 비슷, 단일 프로세스
- 랜더러 프로세스: 브라우저 + 노드 사용 가능, 창마다 별도의 프로세스

        안드로이드에서의 로직과 화면단의 분리가 생각남

## ProtoPie

이웅재 님의 회사에서 개발중인 서비스, Electron + TypeScript로 구축

소스 보호를 위한 `enclosejs` + `pkg` 사용

보통 보안상 코드 보호이 필요한 경우
- 로그인 토큰 및 정보
- 서버 접속 방식
- 비즈니스 로직

Electron에서 제공하는 보안 - 사실상 무의미
- asar pack / extract: 보안의 의미 x
- uglify: 기본적인 것

## enclosejs

Igor Klopov

노드 프로젝트를 바이너리 실행파일로 만들어줌 (유료)

`zeit/pkg` 사용하도록 하고 돌연 **서비스 중단** (오픈소스)

    zeit에 대해 araboja

## zeit/pkg

Node.js 프로젝트를 패키징 > Node.js 설치되지 않은 장치에서도 실행할 수 있게 해주는 [프로젝트](https://github.com/zeit/pkg)

플랫폼 별로 실행파일이 떨어짐

## 실제 솔루션에 적용해보자!

`pkg`가 `Electron`을 위한 솔루션이 아니기 때문에, `Electron`에 적용을 위해선 bridging이 필요함

비즈니스 로직은 `pkg`로 바이너리화 하고, 랜더러 프로세스에서 `node-ipc`로 통신하도록 구현

코드량이 증대되지만, 바이너리 로직은 보호 할 수 있음

    간략하게 훑어주시는 구현 코드

1. 타입스크립트 컴파일
2. `pkg`로 바이너리화
3. `electron-builder`로 실행파일 만들기

## 단점 or 보완점

1. 코드가 많아져 관리가 어렵다 > 여러분 타입스크립트 쓰세요! vscode와도 궁합이 좋다!
2. 용량 문제 > Electron으로 앱을 빌드 할 경우 실행환경까지 가져가기 때문에 원래 용량이 꽤 크다.
3. 엔진 성능 이슈 > `pkg` 자체의 문제 + 최신 스펙의 경우 10% 가량 차이
4. ipc 성능 이슈 > 경유지가 있으니 당연, 브라우저 내 돔 조작 효율화가 더 관건

        설계 자체를 electron 내부 흐름과 동일하게 하여 electron에서 기능이 자체 지원 될 경우의 전환 효율성을 미리미리 고려하신다는 느낌을 받음
