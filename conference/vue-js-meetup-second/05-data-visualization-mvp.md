# 나홀로 데이터 시각화 MVP 만들기 by 김한웅 님

[Max의 온라인 강의](https://www.udemy.com/vuejs-2-the-complete-guide/?siteID=je6NUbpObpQ-Gxcz4rbCS8Kk.HLdS2ozHg&LSNPUBID=je6NUbpObpQ)로 Vue.js 습득 - [깃헙 튜토리얼](https://hanwong.github.io/2017/04/08/vue-stock-trader-01/)

디자이너로 시작, 프론트엔드 개발자로서의 어플리케이션 개발기

## 어플리케이션 구성
- 로그인 - 별도의 플러그인을 간단하게 만들어 사용
- UI 라이브러리 - [ElementUI](http://element.eleme.io/)

## 상세개발기

Vue.js 컴포넌트 간 과다한 렌더링을 방지하기 위한 테크닉을 공유해주심
- 배열형 데이터의 전달로 인한 컴포넌트 간 과부하를 피하기 위해 `lodash.cloneDeep()` 사용하여 부모 컴포넌트에서 자식 컴포넌트로 전달되는 데이터의 참조 관계를 의도적으로 제거
- 둘 이상 Data Source로부터 데이터를 받을 때 컴포넌트의 개별적인 렌더링을 피하기 위해 `Promise.all()` 사용
- 모든 데이터의 수신이 마무리 될 때까지 반복적으로 요청하도록 recursive promise를 구성

개인적으로 AngularJS로 타인이 개발한 프로젝트를 유지보수 할 때 라이프사이클 관리가 정말 힘들었는데, Vuejs의 경우 라이프사이클 관련 hook 함수들이 잘 구현되어있어 편리했다. 특히 Vue-router에도 자체적인 라이프사이클 훅 함수가 잘 구현되어있음!
