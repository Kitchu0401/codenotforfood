# **Async@Spring** by **이일민**님 [[Youtube](youtube.com/tobyleetv)]
*SpringFramework 하에서 비동기 프로그래밍이 구현되는 흐름과 실제 코드 예제로 구성된 발표.*

## 들어가기 전 - 연관유추
- Singleton: 1
- Dependency Injection: 3 (인젝터, 피인젝터, 매개객체)
- Synchronous: 2+ (함께(무엇과 무엇이) + 시간을(무엇을))

## 동기/비동기 != 블록킹/논블록킹
근본적으로 다른 이야기. 구별 할 줄 알아야 할 것.

# @Async

## Spring에서는.. @Async
- 설정된 상태에서 어노테이션 처리될 경우 비동기로 수행됨
- 일반적인 String 등의 리턴값을 가지지 않음
- void, Future, LisenableFuture, CompletableFuture
    - Future 오브젝트는 결과를 래핑한 객체로, get()이 호출되어 작업이 완료된 순간 값을 반환한다.
- Future는 이중 가장 기본적인 **추상화 방식**, 방식의 종류를 정의한게 x

## LisenableFuture
- 함수형 프로그래밍? addCallback(successCallback, errorCallback)
- 한계: 서로 다른 2+ 비동기 작업의 결과값을 작업 수행에 사용할 수 없음
    - call A -> call B in callback A -> callback B 원래의 방식으로 회귀
        - **Callback Hell**

## CompletableFuture
- thenAccept(callback)

## 주의
- 설정하지 않는다면 `SimpleAsyncTaskExecutor`를 기본 TaskExecutor로 사용
- 매 요청마다 생성하고 폐기하는 비효율적인 TaskExecutor

## 그러면?
- Executor, ExecutorService, TaskExecutor 타입의 빈을 "하나만" 생성하여 사용
- 정의된 TaskExecutor가 둘 이상일 경우 @Async ("myExecutor") 처럼 명시하여 사용

# AsyncServlet

# 비동기 스프링 @MVC

## 스프링에서의 Async handling
- Callable
- WebAsyncTask (Callable + timeout, taskExecutor)
- DefferedResult: (+ @Async = return ListenableFuture)
- CompletableFuture
- AsyncRestTemplate

## CompletableFuture
- 함수형 프로그래밍 방식
- call A then call B with A'result

## AsyncRestTemplate
- RestTemplate의 비동기화
- 비동기, 논블로킹, but not 논블로킹IO
- 별도의 논블로킹IO 라이브러리(ex: Netty)를 사용

# 결론
- 비동기 작업과 API 호출이 많은 @MVC 앱이라면
- Java 8 (람다표현식, 참조형함수)
- 비동기 프로그래밍을 굳이 써먹으려고 하지는 마세요.
- 그래도 쓸거라면
    1. 항상 모니터링 가능한 환경에서
    2. TaskExecutor(쓰레드풀)에 대한 고민과 함께 설계해주세요.