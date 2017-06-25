# 함수형 자바스크립트 프로그래밍
- 부수 효과를 미워함 => 순수 함수를 만듬
- 조합성을 강조함 => 모듈화 수준을 높임

more How less Why

그래도 왜? 를 이야기한다면.. 기술력 상향
- 재미 / 실시간성
- 독창성 / 완성도: 어플리케이션에 적합한 창의적인 사용자경험
- 더 많아져야하는 동시성: 사용성의 증가 (물리적으로 하나의 컴퓨터인 것처럼)
- 더 빨라져야하는 반응성 / 고가용성: auto scaling, 배포 용이성
- 대용량 / 정확성 / 병렬성

## 함수형 프로그래밍은
언어 자체를 함수처럼 여기도록, 함수 개념을 가장 우선순위로
> 함수형 사고방식은 문제의 해결 방법을 동사들로 구성하는 것
> 클로저 프로그래밍의 즐거움

## 순수함수란
외부의 상태(ex. 객체)에 영향받지 않는 함수
``` js
function add (a, b) {
  return a + b
}
```
``` js
// this is not pure function
function add (obj, a) {
  obj.value = obj.value + a
}
// this is pure function
function add (obj, a) {
  obj.value += a
}
```

## **어떻게** 전환 할 것인가?
오래된 미래, 어떻게 해왔는지도 중요

# Start live coding

## 1. 함수형 프로그래밍 개요
``` js
function add_maker (a) {
  // 일급함수: wherever, treat as value
  // Closure
  return function (b) {
    return a + b
  }
}

console.log( add_maker(10)(5) )
```

## 2. 함수형으로 전환하기
``` js
// var users = [
//   { id: number, name: string, age: number }
// ]

// 명령형 코드 case
// for 문을 활용한 예

// 아마도
// 30세 이상 사용자
users.filter((obj) => { return obj.age >= 30 })
// 30세 이상 사용자의 name
users
  .filter((obj) => { return obj.age >= 30 })
  .map((obj) => { return obj.name })
// 30세 미만 사용자
users.filter((obj) => { return obj.age < 30 })
// 30세 미만 사용자이 age
users
  .filter((obj) => { return obj.age < 30 })
  .map((obj) => { return obj.age })
```

## _filter, _map 실제 작성해보기
리팩토링의 핵심
1. 중복을 제거
2. 의도를 드러냄
중복을 제거하면 자연스럽게 나오는 함수?

for문 기반의 코드를 리팩토링하며 작성

-> 함수형 프로그래밍에 익숙하지 않은 사람이 익숙한 코드를 리팩토링하며 보여주는 진행방식

_filter > _map > _each 순서대로 리팩토링
``` js
function filter (users) {
  var temp_list = [];
  for ( var i = 0; i < users.lenth; i++ ) {
    if ( users[i].age >= 30 ) {
      temp_list.push(users[i])
    }
  }
  return temp_list
}

function _filter (list, predicate) {
  var new_list = [];
  for ( var i = 0; i < list.length; i++ ) {
    if ( predicate(list[i]) ) {
      new_list.push(list[i])
    }
  }
  return new_list
}

var age_over_30 = _filter(users, function (user) => { return user.age >= 30 })

// 대입문을 제거 - 보다 선언적?
console.log(
  _map(
    _filter(users, function (user) => { return user.age >= 30 }),
    function (user) => { return user.name })
)
```
함수형 프로그래밍: 추상화의 단위 -> 함수

테스트의 용이성: 객체를 통한 프로세스 전체 테스트 불필요, 개별 함수 단위 테스트 가능

함수형 프로그래밍의 테스트는 아무때에나 이루어져도 ok

## 기존의 filter 등의 함수는??
다음의 함수는 함수평 프로그래밍인가?
``` js
[1, 2, 3].filter(function (num) => { return % 2 === 0 })
```
`[1,2,3]`이란 객체가 존재해야하기 때문에 순수한 의미의 함수형 프로그래밍이 아니라고 생각

함수형 프로그래밍이라면 적어도 독립적으로 존재해야함.

객체에 종속 받는 `filter()` 등의 배열 함수, `document.querySelector`의 예

`_each()`의 경우 넘겨받는 대상이 무엇이냐는 상관없이
1. length라는 값을 가지고 있고
2. length가 숫자형 값일 경우
대상의 크기만큼 순회하는 보다 자유로운 함수

    결과적으로 제약이 적어지고, 다형성은 높아짐

** 쉬는시간 **

## 커링
_curry

[커링이란?](http://anster.tistory.com/144)

``` js
function _curry (func) {
  return function (a) {
    return function (b) {
      return func(a, b)
    }
  }
}

// 사용 예: add_maker
var add = _curry( function(a, b) {
  return a + b
} )

// variation: 인자에 따른 즉시실행
function _curry (func) {
  return function (a, b) {
    return arguments.length > 2
      ? func(a, b)
      : function(b) { return func(a, b) }
  }
}
```

_curryr
``` js
// curryr의 의미: 함수의 선언적 타당성 보충
// 생각의 layer를 옮기는 습관이 필요함
function _curry (func) {
  return function (b, a) {
    return arguments.length > 2
      ? func(b, a)
      : function(a) { return func(b, a) }
  }
}
```

_get
``` js
// preventing 'is not a function or property of undefined'
function _get (obj, key) {
  return obj === null ? undefined : obj[key]
}

var _get = _curry(function (obj, key) {
  return obj === null ? undefined : obj[key]
})

// ..
```

_reduce (접는 함수?)
[재료, 재료, 재료] > 요리
``` js
function _reduce (list, iter, memo) {
  _each(list, function (val) {
    memo = iter(memo, val)
  })
  return memo
}
```

_pipe (function chaining)
``` js
function _pipe () {
  var fns = arguments
  return function (arg) {
    return _reduce (fns, function (result, fn) {
      // 넘겨받은 function을 차례대로 호출하는 chain을 반환
      return fn(result)
    }, arg)
  }
}

// 즉시실행형
function _go (arg) {
  var fns = _rest(arguments)
  // _rest = function (list, count) { return list.slice(0, count || 1) }
  return _pipe.apply(null, fns)(arg)
}

// 즉시실행형 적용: _filter, _map > _go > arrow function
_go(
  users,
  console.log)
```

_each의 외부다형성 높이기 - null을 넣어도 오류가 나지록않도록
- 오류가 발생하지 않으면 디버깅은 어떻게 하는가?
- 비동기 위주의 동시다발적이고 복잡한 어플리케이션에서 문제가 발생한 이후의 디버깅은 불가능?
- 디버깅보다 자잘하고 견고한 함수 단위의 사전테스팅을 우선
``` js
var _length = _get('length')
// 예: accept null 
function _each (list, iteratee) {
  for ( var i = 0, len = _length(list); i++ ) { iteratee(list[i]) }
}
_each(null, function (v) { console.log(v) })
```

http://www.globalnerdy.com/wordpress/wp-content/uploads/2016/06/map-filter-reduce-in-emoji-1.png
https://atendesigngroup.com/blog/array-map-filter-and-reduce-js

# 컬렉션 중심 프로그래밍
하위함수들을 함수형 프로그래밍으로 리팩토링하기

# 자바스크립트에서의 지연 평가
실제로 호출되는 시점에 평가?
가로형 수행 x 세로형 수행 o
Stateless
