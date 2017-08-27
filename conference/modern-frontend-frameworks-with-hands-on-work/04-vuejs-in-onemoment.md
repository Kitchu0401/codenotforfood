# 원모먼트의 Vue.js 적용기 by 김우현 님

온라인 당일 꽃배달 서비스 [원모먼트](https://www.1moment.co.kr/)에서의 레거시 대비 Vue.js 도입기

## Vue.js의 장점

Template + Script + Style이 통합된 단일 컴포넌트

[완벽하게 한글화 된 공식 문서](https://kr.vuejs.org/index.html)를 정독하고 하루 만에 바로 적용 가능

친절한 국내 커뮤니티 - [Vue.js Korea Slack](https://vuejs-korea.signup.team/)

## 원모먼트의 레거시

1. 서버사이드 아키텍쳐 구조
    - 파이썬이 주력언어가 아닌 백엔드 개발자 한 분이 개발한 Django 기반 백엔드

2. 메인페이지에 진입하기 위한 쿼리문의 숫자: **421** 건

3. 결제 오류
    - 정상적인 결제 루틴: Order Sheets > PG > Status Change (네트워크 오류로 인한 중결함 발생)
    - 원모먼트 결제 루틴: PG > Order Sheets > Status Change

## Vue.js를 도입하며

프론트엔드와 백엔드를 분리, 프론트엔드에 Vue.js를 도입

사이트 응답속도 크게 개선 및 Bad Request 현상 대폭 감소

## 오픈소스 등록하기

[Vue.js 음력 달력 컴포넌트](https://github.com/KimWooHyun/vue-lunar-calendar)

오픈소스 개발과정
- Webpack 설정
- 소스 작성
- 데모 작성
- 데모 사이트 올리기: Github page
- README.md
- 배포하기: `npm publish`
- 확인하기: https://npmjs.com/package/my-package-name

개발만으로 끝나지 않고, 오픈소스로서 확장됨
- Npm package로 배포 후 Vue official tweet에 소개됨
- [Awesome Vue.js](https://github.com/vuejs/awesome-vue)에 컴포넌트 등재 PR을 보내고, 승인됨!
- 다국어 처리를 위한 설정 추가 후, 이탈리아에서 i18n 관련 PR을 받음.
