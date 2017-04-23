# **Spring WebFlux** by **이일민**님 [[Youtube](youtube.com/tobyleetv)]
*이 세션부터 코드 본떠두려다가 속기 붕괴 시작..*

## 언제?
- 비동기-논블록킹 리액티브 개발 (고성능)
- 서비스간 호출이 많은 마이크로서비스 아키텍쳐

## 무엇이 다른가?
- 개발방식
    - @MVC 어노테이션 방식
    - 함수형 모델 (RouterFunction, HandlerFunction)
- 새로운 요청-응답 모델
    - 서블릿 스택&API -> 리액티브 함수형 스타일
    - ServerRequest, ServerResponse

## 함수형 스타일의 요청 매핑
``` java
@FunctionalInterface
public interface RouterFunction<T extends ServerReponse> {
    Mono<HandlerFunction<T>> route(ServerRequest request);
}

@FunctionalInterface
public interface HandlerFunction<T extends ServerResponse> {
    Mono<HandlerFunction<T>> route(ServerRequest request); // missing
}
```

## 함수형 WebFlux가 웹 요청을 처리하는 방식
### RouterFunction
- 요청 매핑
### HandlerFunction
- 요청 바인딩
- 핸들러 실행
- 핸들러 결과 처리(응답 생성)

``` java
// HandlerFunction helloHandler = req -> {
//     String name = req.pathVariable("name");
//     Mono<String> result = Mono.just("Hello " + name);                           // Mono -> Reactor
//     Mode<ServerResponse> res = ServerResponse.ok().body(result, String.class)   // body, header, status
//     return res;
// }

HandlerFunction helloHandler = req ->
    ok().body(fromObject("Hello " + req.pathVariable("name")));

RouterFunction router = req -> 
    REquestPredicates.path("/hello/{name}").text(req)
        ? Mono.just(helloHandler)
        : Mono.empty();
```

->

```
RounterFunction router =
    RouterFunctions.route(
        RequestPredicates.path("/hello/{name}"),    // requestMapping
        req -> ServerResponse.ok().body(
            fromObject("Hello " + req.pathVariable("name")));   // responseCallback
    )
```

->

```
// 속기붕괴 망했ㄸㅏ.....ㅜㅜㅜㅜ
@Bean
```

```
// 여기도 망했습니다 ㅜㅜ
## ChainRouting
public RouterFunction<?> routingFunction() {
    return nest(pathPrefix("/person"),
        next(accept))
}
```

## 장점
- 모든 웹 요청 처리 작업을 명시적인 코드로 작성 (메소드 시그니쳐 관례, 타입 체크 수행)
- 함수 조합을 통한 편리한 구성, 추상화에 유리
- 테스트 작성의 편리함

## 단점
- 함수형 스타일의 코드 작성

## WebFlux만으로? 서비스 속도 향상을 위해 다음을 개선해야
- 데이터 액세스 리포지토리
- HTTP API 호출
- 기타 네트워크 사용 서비스 