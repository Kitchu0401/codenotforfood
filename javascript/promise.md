# Promise 정리 ()

## Usage
```
// Promise 함수 생성

// *** 주의: Promise 생성자에 파라미터로 넘겨진 함수는 즉각 실행되고, 그 상태를 유지함 ***
var _promise_status_preserved = new Promise(onFulfilled, onRejected) {

        ...

    if ( ... ) {
        // success
        onFulffiled(value);
    } else {
        // failure
        onRejected(reason);
    }
};

var _promise_status_liberated = function() {
    return new Promise(onFulfilled, onRejected) {

        ...

        if ( ... ) {
            // success
            onFulffiled(value);
        } else {
            // failure
            onRejected(reason);
        }
    };
};

// Promise 함수 사용
promise.then(
    function(value) { /* fulffilment */ },
    function(reason) { /* rejection */ }
);

// 성공만 처리
promise.then( function(value) { /* fulffilment */ } );

// 실패만 처리
promise.catch( function(reason) { /* rejection */ } );
```

## States
A promise must be in one of three states: pending, fulfilled, or rejected.

Promise는 다음의 상호배타적인 세 가지 상태를 가진다.

1. When pending, a promise:
    - may transition to either the fulfilled or rejected state.
2. When fulfilled, a promise:
    - must not transition to any other state.
    - must have a value, which must not change.
3. When rejected, a promise:
    - must not transition to any other state.
    - must have a reason, which must not change.

Here, “must not change” means immutable identity (i.e. ===), but does not imply deep immutability.

promise가 비동기 함수(일회성 결과)에 유용한 점은, promise상태가 한 번 확정되면 **더이상 변하지 않게 된다**는 점이다.

## 참고 링크
- [Promises/A+](https://promisesaplus.com/)
- [ES6 비동기 프로그래밍](http://webframeworks.kr/tutorials/translate/es6-async/)
- [바보들을 위한 Promise 강의](http://programmingsummaries.tistory.com/325)
    - then()과 catch()의 흐름에 대해 잘 정리된 그림 참고 가능