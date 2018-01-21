# Angular 기본 개념 잡기 by 한장현 님

심화 과정을 준비했다가 Angular에 대한 두려움을 가진 개발자가 있다는 것을 실감

Angular의 기본 개념과 지원하는 내용에 대한 기본적인 세션을 구성하기로 결정

## Angular는 AngularJS는 다르다

TS를 도입하면서 프레임워크 이름 변경

버전 정책은 [SemVer 관련 한장현 님 포스트](http://han41858.tistory.com/22) - 버전 숫자에 겁먹을 필요 x

디렉티브 기반에서 컴포넌트 기반으로 전환되었지만 철학과 개발방식은 비슷

## Angular는 종합 프레임워크

어플리케이션 구조 전체를 아우름

각 모듈의 정합성과 자연스러운 데이터 연결 보장

MEAN 스택에서 프론트엔드 - 백엔드 - 데이터베이스까지 JSON 객체만으로 데이터의 흐름을 제어 가능한 느낌과 비슷함

## 프론트엔드 SPA

페이지 내부의 이동을 라우터로 지원 - 전통적인 HTML 이동과 다름

딥링크 지원

## Typescript

Javascript superset

정적타입, 제네릭, 인터페이스, TSLint

개인적으로 개발편의성보다는 유지보수성에 더 도움이 된다고 생각

## Angular는 컴포넌트 기반이다.

추상화된 DOM 엘리먼트
- 코드의 분할
- DOM에 직접 접근은 추상화의 장점을 살리기 위해 지양하는 것이 좋음

어노테이션으로 Angular 컴포넌트 등록
- 객체의 생성 및 주입은 Angular가 관리
- 라이프사이클 함수를 지원

## 데이터 바인딩

AngularJS에서 가장 인기있던 기능이지만, 성능이슈의 단골이었음
- Angular에선 성능 향상을 위해 단방향 바인딩이 기본
- 양방향 바인딩도 물론 가능합니다!

## 옵저버블 지원

콜백 체인 > Promise 체인 > Async 체인 > Observable 체인 (RxJS 내장)

데이터 스트림에 사용
- 키보드 입력 이벤트, 서비스 상태 전달에 적합
- Http보다는 WebSocket에 더 어울림
- Http 기반 환경에서는 효율성을 고려 할 경우 기술 스택이 중복 될 가능성이 있음 (Observable vs Promise)

## Angular는 서비스 & 의존성 주입을 지원한다.

컴포넌트 간의 연결을 전역 데이터 풀로 홀용 가능

생성 방법을 등록하면 이후는 선언만 필요

더미 객체를 사용하는 **단위 테스트**에 유리

## Angular는 모듈화를 지원한다.

ES6 모듈의 연장, 대체는 아님

`@NgModule`은 다양한 형태의 모듈링을 지원
- Angular에서 제공하는 모듈: `import`
- 사용자가 만든 컴포넌트: `declarations`
- 객체 생성이 필요하면: `providers`
- 시작 컴포넌트는: `bootstrap`

## Angular는 최신 트렌드 도입에 적극적이다.

프론트엔드 최신 트렌드
- 웹 컴포넌트
- PWA: [PWA 관련 한장현 님 번역 포스트](http://www.bloter.net/archives/274549), [블로터 ITKerword](http://www.bloter.net/archives/274549)
- 크로스 플랫폼
- 리액티브 프로그래밍 (+ Nativescript)
- 서버사이드 렌더링
- 머티리얼 디자인
- Angular CLI
- [Augury](https://augury.angular.io/): 디버깅 & 프로파일링을 위한 Chrome Extension 툴

## 지금 공부해야 할 것, 앞으로 공부해야 할 것

지금 공부해야 할 것
- Typescript
- Augular 프레임워크 (기본적인 선언, 라이프사이클 정도만 알아도 충분)
- 컴포넌트 기반 설계

앞으로 공부해야 할 것
- **Webpack** 최적화
- SSR, SEO
- 머티리얼 디자인 & 애니메이션
