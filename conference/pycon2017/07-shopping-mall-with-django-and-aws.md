# Django/AWS를 이용한 쇼핑몰 서비스 구축

기술적인 부분보다 비즈니스적인 부분에서 서비스 개발시 포커싱해야하는 부분을 잘 설명해주심

## 쇼핑몰, 직접 구축 할 것인가?

쇼핑몰을 직접 만들겠다면, 신중하게 고려해볼 것
- 장점: 차별화된 UI/UX, 프로모션과 함께 방문 고객에 대한 세밀한 분석 가능
- 단점: 기존 서비스를 제공하는 업체에 의뢰하면 구축 & 유지보수에 소모되는 시간과 노력을 절감 할 수 있음

> Why reinvent the wheel?

## Django

다양한 웹 개발 패키지

사용하기 쉬운 ORM

풍부한 Third-party 생태계

## 데이터 모델링에 대한 고민

고객, 물류, 관리자 합해 attribute 30개

핵심 attribute만 남기고 기능적 구분에 따라 모델들을 분리, 핵심 모델을 참조하도록

카테고리 관련된 multi-depth-hell: `Django-mptt`

쇼핑몰의 핵심 모듈 장바구니: `Django-carton` - 추가적인 기능은 라이브러리를 확장하여 개발

## 주문/결제

PG(결제 모듈) 직접 연동 - **"Don`t do that"**

대신 `I'mport` 쓰세요!

## 관리자 페이지

관리자 페이지 100% 직접 구현은 힘듦 vs Django admin은 일반적으로 사용하기 불편

목적 및 사용 대상에 따라 Django admin / 자체 제작 UI로 이분화하여 사용

Django admin을 보완하기위해 `Django-grappeli`

개발을 모르는 관리자가 html을 편집할 수 있게 해주는 기능을 제공하는 `Summernote`를 파이썬 플러그인인 `Django-summernote`를 사용하여 적용

UI의 경우 각자 사정에 따라 다르겠지만 Bootstrap 기반의 `AdminLTE`를 추천

## 매출통계

복잡한 쿼리 구축 `Django Aggregation`

Django Queryset Redis 캐싱 `Django-cacheops`

시각화는 `Google Chart`

## 비동기 작업 / 작업 스케쥴링

비동기 작업: 고객의 액션과 함께 트리거 - Blocking을 유발하는 작업들 / 실행 시간이 긴 작업

작업 스케쥴링: 일정 주기마다 자동으로 수행되어야 하는 작업들

`Celery`

## AWS

소규모 개발팀에서는 필수적인 클라우드 환경

## AWS Elastic Beanstalk

개발된 코드를 업로드하기만 하면 서비스를 올려줌

개벌언어와 버전에 따라 일종의 Template을 제공

GUI 기반 다양한 설정 가능

쇼핑몰에서 큰 비중을 차지하는 static resource를 **S3**에서 제공하도록 완전 분리
