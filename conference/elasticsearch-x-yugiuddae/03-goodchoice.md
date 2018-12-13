# 여기어때

서비스 운영과 모니터링 관점에서의 es 활용 (오픈소스)

PHP + Flask + RDS + ES

NGram + 은전한잎 -> 

1. 검색 요청

2. 내부 Flask Search API 요청

3. RDS에 먼저 조건에 맞춘 필터링

4. ES로 요청

= 좋지않음

검색 / 시스템 모니터링 / 로그 수집 및 분석 / aws resource utilization 모니터링 / 비용 추적 및 분석

추천 / 머신러닝 / 딥러닝 예정

구축:

검색 서비스 구축 -> 검색에서 생성되는 로그 적재 및 분석 -> 전사적 로그 및 모니터링 통합

AWS 비용 관측 + AWS RI 관리 + 전사 로그 수집 및 분석

매니징과 readonly 형태로 구분해서 운영

### 구축하며 겪었던 문제나 삽질

aws ec2 인스턴스 뽑기

- 인스턴스에 대한 문제점 확인 자체가 문제

hot-warm 적용시 shard allocation issue

- 장비 사양 문제, 좋은 장비 쓰세요. 장비 성능이 좋지 않아 shard allocation 시점에 마스터 노드가 메타데이터를 인식하지 못하는 이슈

mapping 설정시 similarity issue

- 6.5버전대에선 해결됨. 6.3 버전까지는 sim 관련 설정이 있을 경우 index update시 오류 발생

EBS IOPS Credit 소진에 따른 색인 성능 저하 문제

- 스트레스 테스트시 색인 성능 저하에 대한 인식 부족. Provisioning IOPS 사용 (aws?)

script 사용시 데이터가 적음에도 불구하고 loop 성능 저하 문제

- 날짜별 range 쿼리 수행시 속도 저하 문제, index의 시작과 끝만 검색하도록 개선. 코드 개선 이전엔 primary shard size를 늘림

- 단순히 샤드의 볼륨만 늘린 상태에서 script를 사용하면 성능 상의 문제가 발생 할 수 있음을 명심 할 것

하루 평균 4천만건의 로그 데이터 저장 및 실시간 분석 문제 (40s 가까이)

- 데이터 노드 2개에서 5개 (사양 다운사이징)

- primary size 20gb > 5gb: 분석 질의를 많이 사용하기 위한 구성, 오버헤드 관련 이슈?
