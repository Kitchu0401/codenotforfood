# References

## APIs

1. [Google Cloud Speech API](https://cloud.google.com/speech/)

  - 80여 개 언어 지원
  - Client library (static audio file only?), RPC package, Rest API 형태로 제공
  - Sync, Async, Streaming 방식
  - 요청 500건 / 100초, 요청 250,000건 / 일, 5,000초 / 100초, 480시간 / 원

2. [Naver Clova Speech Recognition (CSR)](https://developers.naver.com/products/clova/vrecog/)

  - 4개 언어(한국어, 영어, 일어, 중국어(간체)) 지원
  - Android & iOS SDK 형태로 제공
  - 자체 구현된 스트리밍 프로토콜 방식
  - 3,600초 / 일