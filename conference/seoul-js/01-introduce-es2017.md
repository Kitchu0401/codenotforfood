# ES2017 (ES8) 소개 by @june

## Minor 1: Object.values vs Object.entries

An array of strings that represent all the enumerable properties of the given ovject.

- Object.values: 밸로가 원소인 배열
- Object.entries: 키, 밸류 페어인 배열의 집합

## Minor 2: Padding

- String.prototype.padStart
- String.prototype.padEnd

## Minor 3: Object.getOwnPropertyDescriptors

A property descriptor of the given property if it exists on the object, `undefined` otherwise.

## Minor 4: Trailing commas in function parameter lists and calls

불필요한 syntax error 및 코드 변경 내역 추적 용이

## Major 1: Async functions

대표적으로 callback hell > Promise > **Async**

Promise 로 지원되던 비동기 지원을 지시어의 레벨까지 끌어올렸다는데에 의의가 있음

``` js
// still usable helper functions
Promise.all(a, b, c);
// why not?
await all a b c;
```

에러 핸들링에서 이점

## Major 1: 메모리 공유성 & 원자성

### 메모리 공유성

고려되었던 방식들:
- Cpu to Cpu > bit 전송
- Memory to Memory: Create memory - 메모리의 중복 사용으로 비효율적
- Memory to Memory: Transfer memory - 이전되기 이전의 출처에 접근 불가

결론: SharedArrayBuffer (<> ArrayBuffer)
- 워커들과 공유 가능
- 작업량 / cpu숫자 의 기대효용보다 조금 더 낮은 효율 (cache가 중간에 위치하기 때문)

        결국 병목이 여전히 존재한다는 이야기?

        병목의 단계가 cpu > memory > cache로 점점 경량화 되어가는지

### 원자성

SharedArrayBuffer로의 접근을 일시적으로 제한함으로써 공유된 자원의 원자성을 확보

    자바 `synchronized` 키워드와 비슷한 개념인지
