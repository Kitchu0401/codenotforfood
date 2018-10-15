# 누구나 만드는 내 목소리 합성기 by 이봉준 (Naver Voice)

자신의 목소리를 합성할 수 있는 서비스 nVoice 구축 사례 (NES)

텍스트로 입력하는데에는 주체 별 차이가 없지만, 소리내어 읽을 경우는 다르다 > 음성은 텍스트가 가지지 않은 정보가 많음

음성 합성이란: 발음, 속도, 호흡, 운율 등의 정보를 추측해 화자와 비슷한 목소리를 생성하는 것을 목표로 함

## nVoice - Concatenation Synthesis

화자의 음성을 잘게 분할하여 저장, 동적인 텍스트 정보가 들어왔을 때 적절한 음성을 찾아 조립 후 반환

- Target code: 얼마나 비슷한가?

- Join: 연결성

## Process

1. 화자 선정: 호감 + 발음의 정확성 + 목소리의 일관성, 자연스러움

2. 발성 스크립트 선정: 특이한 케이스를 최대한 피한다는 느낌: 스크립트를 읽기 쉽게, 모호한 발음 알려주고 + 어휘를 보강함

3. 녹음: 적당한 볼륨, 노이즈 제거

4. 전사(transcription): 녹음된 음성을 실제 발음열에 따라 분할된 음성 정보로 저장하는 과정

5. 언어 처리 모듈

  - ...

6. 운율 모델링

 - Pitch: 목소리의 톤
 - Energy: 강세
 - Duration

7. 음소 접합: 찾아서 - 융통성있게 붙이고 - 스무딩

## nVoice

1. Language Understanding Module

2. Prosody Prediction Module

3. Unit Selection Module

## 개인화 음성 합성

개인의 기호에 따른 음성 서비스

현재까지의 기술로는 일단 긴 시간의 녹음 데이터가 필요함

짧은 시간의 녹음으로 개인의 특성을 반영한 목소리 합성이 목표

### Why?

0. 전사작업에 들어가는 막대한 비용

1. 일반인 개인 화자 선정시의 문제

2. 녹음 환경의 문제

기존의 막대한 규모의 전사 작업을 개인이 수행 할 수 있는가의 문제

구현 상의 문제

-> 현재의 방법으로는 어렵다

## 어떻게 문제를 븍복했는가?

1. Statistical Parametic

기존의 모든 음소 조합이 필요한 방식에서 탈피: Statistical Parametic 방식으로 전환

(음성 / 텍스트 데이터 베이스에서) Feature Extraction > Model Training > Statistical Model

Parameter:

- Voice / Unvoice (유성음 / 무성음)
- F0 (Fundamental Frequency) 기반이 되는?
- LSF
- BAP (둘 다 차원축소를 위함)

2. End-to-End

- 네트워크: Attention 기반 seq2seq 네트워크
- 어떤 부분을 추정하는가? Mel spectrogram
- 어떻게 소리를 만드는가? Griffin-Lim

3. Vocoder? (WaveNet x)

품질이 살짝 아쉽지만, 합성과 학습속도를 고려한 선택

단점을 보완하기 위한 보완책들

보완이 어려운 부분은 과감하게 타협 (Voice / Unvoice 혼동)

4. Speaker Adaptation

대량의 추가적인 음성 데이터 + 소량의 개인 음성 데이터를 활용한 모델 구축

묵시적(Implicit Adaptation)

## 음성 합성 기술의 과제

품질

전처리 기술 고도화, 더 적은 데이터 (개인 전사 작업의 편의성)