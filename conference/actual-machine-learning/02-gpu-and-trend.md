# GPU Trend와 딥러닝

Nvidia 근무하시는 한재근 님

## GPU에 대한 소개

No more free lunch - 집적도를 높이는걸로는 성능 향상 한계계

앞으로도 성능향상의 격차는 더 커질 예정

의외로? 혹은 당연하게도 GPU 시장의 가장 큰 고객은 물리역학, 항공우주학 분석 등. 실제 우량고객은 석유회사 (채굴)

대중들이 바라보는 GPU 특화 task는 딥러닝 / 비트코인 / 그래프분석?

구글의 머신러닝 투자로 인한 GPU 매입 - 엔비디아 동반성장

## 엔비디아의 시장 확보를 위한 노력

쿠다 개발 및 공개, 지속적인 라이브러리 및 SDK 개발

엔비디아 파스칼 아키텍쳐에 대한 소개

Heterogeneous Computing 개념 - 행렬연산 부분을 GPU에게 위임

## 실전 GPU 이야기

CPU 살 때: PCI Express Bus가 충분한지 고려 - GPU의 성능을 최대한 끌어내기 위해

## Next GPU Volta

2017 GDC에서 공개

폭발적으로 증가하는 뉴럴 네트워크 복잡도
- 2017년 구글 다국어 번역에 투입되는 파라미터 크기 - 8억 7천만개(슬라이드상 8,700m), byte로 나타내면 32기가

올해 말 출시 예정인 차세대 GPU Volta에 대한 설명

## GPU 서버에 대해서

CPU - Switch - GPU 아키텍쳐