
Transfer Learning
- 기존의 만들어진 모델을 사용, 빠른 학습과 예측률 향상
- 개를 식별하는 모델에 추가로 학습을 시켜 고양이를 식별하는 모델로 활용
- 이미 잘 훈련된 모델이 있고, 특히 해당 모델과 유사한 문제를 해결시 transfer learning을 사용

Fine Tuning
- 모델의 parameter를 미세하게 조정
- 조정이 필요한 레이어만 별도로 학습
- Fine tuning 수행시 주의점
  - 러닝레이트 낮게
  - 변화는 최소한 조금씩
  - 기존의 잘 학습된 모델을 망칠 수 있기 때문에 주의를 요함
- Hyper parameter 튜닝

Ensemble
- 여러 모델을 이용해 데이터를 학습한 후, 결과를 평균하여 예측 (정확도 4-5% 향상 기대)
  - Voting: 모델들 각각이 추출한 정답을 다수결로 결정
  - Bagging: Data를 Random Sampling으로 분할하여 모델 학습 후 최종 결과를 추출
    - Random Sampling시 특정 데이터 군에 학습 결과가 편중 되는 Issue
  - Boosting: Random Sampling 기반, 이전 모델들이 예측하지 못한 Error 데이터에 가중치를 부여
  - Stacking:
- 연산량이 증가하는 단점이 있으며, 이를 보완하기 위한 방법도 다수 존재

Network-in-Network
- 네트워크 층의 추상도 향상을 위해 선형성을 비선형성으로 만드는 네트워크 구조 (특히 Conv Layer)
- 구글의 GoogleNet
