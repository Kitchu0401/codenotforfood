# 네이버 검색과 개인화 by 최재걸 (Naver 통합검색)

## 네이버는 왜 이제서야?

네이버가 개인화를 추진하면서 고민했던 부분들

- Privacy: 개인화가 익숙한 시대 - 불편함보다 편리함이 앞서야
- Filter Bubble: 개인화에 갇히는 문제 (구글의 경우 10%, BING 15% 가량)

## 검색의 목적

검색의도에 맞게

개인화가 없이 이룰 수 있는 검색 품질을 완성: 이제 개인화뿐이야

최대 다수의 최대 만족 -> 의도 분류 결과에 따른 검색 결과들을 복합적으로 나타냄 but 모든 사용자에게 같은 화면을 출력 할 수 밖에

검색 개인화의 적용:

- 최대 다수의 최대 만족 > 개인의 최대 만족
- 검색 의도에 맞는 결과 제공 (뉴스기사? 이미지? 동영상?)

Click Entropy: 의도의 확산성? (80%)

### 네이버는

**3-Level Query Ambiquity (95%)**

질의가 들어왔을 때

1. Entity 검색 결과 엔티티 분류
2. Property 검색 결과에 대한 프로퍼티 (사진? 영상?)
3. Document 프로퍼티 상세화 (전신사진? 이미지 사진?) - not yet

왜 Document level이 어려울까? 결국, 정확한 검색 의도의 파악이 쉽지 않기 때문

검색의 개인화는 사용자의 검색의도를 정확히 파악 할 수 있을 때!

## 개인의 검색 의도 파악

사람의 기억 방식(short term / long term)과 유사하게 3계층으로 (HuMM: Human Memory Mirror)

- Immediate Memory: 네이버 이용 기록 (실시간 급상승?)
- Working Memory: 의미를 가지고 연속되는 일련의 행동 (세션 내에서 의도를 가지고 행동 할 때)
- Long Term Memory: 행동 패턴 (반복되는 working memory)

> 주식에도 관심이 많고, 보통 주식을 검색하지만 실시간 검색 키워드로 가수가 떴다면 검색 의도가 가수 쪽에 있을 확률이 높다

> 하지만 이 경우, 사용자가 직전에 다른 회사의 주식을 검색했다면 주식 관련 질의일 가능성이 높다

즉, 3계층이 적절하게 협의하여 의도를 파악함

적용 결과: 클릭 비율 증가, 스크롤의 감소

## 그럼에도 불구하고.. 어려운 점

데이터가 Sparse하다:

- 검색 횟수가 부족함
- 세션 기반 검색 횟수 부족함 -> 검색 품질이 좋을수록 개인화가 어려움?

## 개인화 검색 확장 예정 (금년 하반기)

1. User Group: 유저 간 long term memory 사용해 확장 - 협업 필터링?

2. Query Group: 유사 쿼리 ???

## 2019..

검색 요구 좀 더 반영! 과감하게

네이버 자체의 검색 템플릿을 벗어나 UI적인 측면에서 경험 탈피
