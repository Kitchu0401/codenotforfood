# Papago Internals: 모델분석과 응용기술 개발 by 신중휘 (Naver 기계번역)

기계번역 서비스 팀 구조?

## 파파고와 함께: 학습과 수렴 by (정권우)

### Transformer

1. 인코더에서 각각의 단어를 벡터로 변환하고, 이를 취합하여 문장 레벨의 벡터로 변환

2. 디코더에서 문장 레벨의 벡터를 전달 받아 전개가 끝날 때까지, 번역된 이전 단어와 벡터를 참고하여 단어를 출력

매우 학습하기 어렵고, 민감한 모델이다

### 개괄적인 기계번역의 학습과 수렴의 프로세스

어떻게 파파고는 기계번역의 품질을 측정하고 개선하는가?

**문제점 1)** 최신 논문 수렴 기준: 300,000 / Learning Rate 기반 -> 정해진 기준이 없다

그나마, **BLEU** 점수: 원문과 번역문을 문자열 기준으로 평가

1. 다양한 학습 방법론 실험
2. 매 iteration마다 BLEU 점수의 추이 확인

**문제점 2)** BLEU 점수가 높다고 번역 품질이 높지는 않다

좋은 품질의 번역이란:

- 동일한 의미
- 자연스러운 문장
- 2개 국어가 능통한 전문가

BLEU vs 전문가 평가 추이는? 낮다

어느 시점의 학습 모델을 선택해야 전문가 평가와 일치하는 좋은 결과를 얻을 수 있을까?

### 앞으로는

물론, 서비스 품질 / 속도 개선

## 인공신경망을 활용한 웹사이트 번역 by 김재명

### 웹 번역의 프로세스는?

텍스트만 떼어 번역하면 원문의 태그들을 살릴 수 없으므로, 최소한의 문장 단위를 보존 한 채로 번역해야함

-> 신경망을 활용해 번역 한 후, 태그들을 *적당한* 위치에 삽입해주는 방식

seq2seq + attention

원문과 번역문 간의 각 단어의 연관성을 attention 기준으로 추론

### 잘 되지만?

attention - word alignment 간의 명확한 상관관계가 존재하지 않음

error propagation: 번역이 잘못되면 태그 복원 성능도 하락

웹페이지 정제, 언어별 휴리스틱, 연산의 병렬 처리

### 개발시의 어려움

유니코드의 그림자 - 같은데 다르고, 다른데 같다: 정규화의 어려움

지저분한 웹 페이지: 웹 표준을 지키지 않는 태그

번역 할 부분만 뽑아내기: 원문이 보존되어야 하는거 / 번역기에는 보내지만 원문 내용 그대로 나와야 하는거 등

- 기본적으로 inline 태그만 고려

언어 별 특성을 고려하면 태그 복원시 좀 더 자연스러워질 수 있다 (한국어: 품사 태깅)

### Process

1. 사이트 쪼개고
2. 쪼개진 트리 전달
3. 텍스트 태그 추출
4. 문장 분리, 태그 위치
5. 번역 분산 요청
6. 분산 결과 리턴 (attention)
7. 태그 복원, 트리 재구성
8. 트리 리턴
9. 번역된 노드 렌더링

### 이슈

원문 중 일부가 누락

원문의 일부가 번역문에 녹아 있는 경우 -> 태그 복원시 어색해짐

### 향후에는

기계 번역기 성능 up

Alignment와 태그 복원 품질 up