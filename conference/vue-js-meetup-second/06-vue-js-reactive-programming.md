# Vue.js와 Reactive Programming by 이선협 님

간단한 연산 코드로 알아보는 Reactive Programming: 변수의 변화를 감지

## Reactive Programming
- Observable - 반응형 그 자체: Observable, Observer, Subscribe
  - Hot Observable - 이벤트를 무조건 발행 (Eager Evaluation)
  - Cold Observable - 구독자가 없을 경우 이벤트를 발행하지 않음 (Lazy Evaluation)

- Data Flow
  - Control Flow - Goto, If / Then / Else, Switch / Case, For / While
  - Data Flow - Stateless, Recursion, Pipe

## RxJS

Observable Chaining Concurrency

RxJS로 구현해보는 Wikipedia 항목 검색 예제

코드

1. `pluck`: value 추출
2. `filter`: 2글자 이상
3. `debounce`: 200ms 마다
4. `distinctUntilChanged`: ??
5. `flatMgLatest`: 마지막으로 도착한 비동기 응답만 처리
 
## Vue-rx

RxJS로 구현했던 Wikipedia항목 검색 예제를 Vue-rx로 바꿔보자!
- `subscriptions`: computed와 다르지 않으나, 
- `$watchAsObservable`: 데이터를 감시하여 변경이 발생할 경우 Observable을 발생시킴
- `v-stream` 디렉티브: Dom element를 Observable로 사용 할 수 있게 해줌

## 비동기의 세계

Promise, async / await와 RxJS와의 비교: 비슷하지만!

차이점
- RxJS는 비동기 작업을 취소 할 수 있음
- RxJS는 데이터 컨트롤을 위한 오퍼레이터 제공
- RxJS는 다수의 이벤트를 제어 가능

## RxJS를 배워야하나요?

> 꼭 배워야 할 필요는 없지만, 알아두면 좋습니다.

Rx는 반응형 프로그래밍 패러다임을 기반으로 만들어졌기 때문에, 패러다임 자체를 습득 할 수 있음!

또한 Rx는 비동기 프로그래밍에 강한 면모를 보여줍니다.
