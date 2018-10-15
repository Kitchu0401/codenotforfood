# 기계독해 QA: 검색인가, NLP인가? by 서민준 (Naver ClovaML)

검색, NLP, 검색 + NLP

## 검색으로 찾는 QA

네이버에 검색

- **질의문과 문서의 관련성**
- 유저의 히스토리
- 문서의 신뢰도와 인기도

등등 다양한 요소를 고려해서 랭킹

### Word Matching

제목에만 적용 할 경우 효과적 / 질의문이 길어질수록 비효율적

TF-IDF, Okapi BM25: 결국, 워드 매칭! 단어가 존재하지 않는다면?

-> LSA

- sparse > dense vector (SVD)
- 각 단어에 추상적인 태그를 할당, 이를 통해 다른 단어끼리도 비교 가능

검색의 한계: 문장을 "읽는" 것이 아님 -> **NLP**

## NLP로 읽는 QA

Goal: 문서 no, 문서를 읽은 후 맥락을 파악해 응답 도출

1. 인풋 / 아웃풋 정의하기

Neural Extractive QA Trend

1. 문장 레벨 QA: 문장 속에 답이 있기 때문에, but 길다
2. 구문 레벨 QA: 답변을 좀 더 간결하게
3. Cross-attention: 문서를 읽으면서 질문을, 질문을 읽으면서 문서를 참고: 인명 나오면 질문 보고, 동사 나오면 질문 보고
4. Self-attention: 문서를 읽으면서 문서를 참고
5. Transfer learning: Unlabeled 데이터 활용 (Wikipedia)
6. 사람을 이기는: 앙상블 + NLP툴 + Data Augumentation
7. Next: Linear time 이슈 - 문서의 길이에 시간이 선형비례

## 검색과 NLP의 접점

### 찾고나서 읽기

검색으로 모수를 줄인 후 답변 도출을 위한 NLP - Linear time problem 극복 (Error propagation?)

### One Solution?

기반 데이터를 정리: Vector화

문서를 NN을 통해 벡터로 매핑, 질문이 들어오면 MIPS(해싱 알고리즘)을 통해 추출

### Phrase Indexed QA 삽질기?

Pipi-line 말고 End-to-End로 해보자!

Bi-LSTM으로 시작, Self-attention으로 확장

**Duality**

**Modality**

- 질/답의 다대일 관계
- 추가적인 변수(Latent Variable)을 적용했지만..

**Scalability**

- SQaUD에서 탈피 (실제 QA시나리오가 아님)

비슷한 엔티티??

## Conclusion


