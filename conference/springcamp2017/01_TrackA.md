# 프로세스와 스레드, NIO 그리고 리액티브 스트림 by **박성철**님
*주: 프로세스 및 스레드, NIO에 대한 개념정리 느낌의 세션이었음.*

## Process, Thread
과거와 현재의 의미가 다름: 관리주체의 역전 (주체의 변화: 프로세스 > os)

## 프로세스와 비교했을 때 쓰레드가 가지는 장점
- 프로세스를 생성하는 비용보다 쓰레드를 생성하는 비용이 저렴
- Heap 메모리 공간을 프로세스 내의 쓰레드 들이 공유 가능

## 쓰레드 단점
- Context switch: 공유된 자원(힙)에 다른 쓰레드가 접근할 때마다 switch가 필요함 (io access)
- 동시 접근성에 수반되는 동기화 관련된 구현 테크닉이 추가로 요구됨
- 프로세스가 아닌 쓰레드 단위로 작업이 분할되면 디버깅에 어려움이 생김

## 쓰레드풀

## Thread in JVM
JVM internal 구글링
JVM 내 쓰레드 비용 (쓰레드 생성비용 + JVM Overhead) + Garbage Collection

## 비동기 프로그래밍, 언제 사용해야하는가?
- cpu 자원을 많이 사용하는 코드: 분할 가능할 경우 병렬화
- io blocking: io작업 요청 쓰레드는 완료까지 대기

## 실전
- class Thread
- interface Runnable

## Java 비동기 프로그래밍의 어려움
- 코드의 흐름을 읽기 쉽지 않고
- 비동기의 결과값을 받기 어렵다 void Runnable.run() -> 쓰레드 동기화 이슈
    - 최초 Heap 영역에 위치하는 객체를 쓰레드 외부에 생성한 후 쓰레드 작업 내에서 데이터를 갱신하는 방식으로 구현

## Java 비동기 프로그래밍 구현
1. wait(), notify()
2. interface Future get(), isDone() from JDK1.5
3. CompletableFuture JDK1.8
    - class CompletableFuture
        - intertace Future
        - interface CompletionStage
    - lamda
    - (+ method reference)
    - + reactiveStream

## NIO
근본적인 문제: ThreadPool Full -> JDK1.7 

## 비동기 Servlet 구현체 변천
- Servlet 3.0 - AsyncServlet
- Servlet 3.1 - Nonblocking IO
- Spring MVC: - DefferedResult

## Event Driven Programming
"우리는 이벤트의 세상에 살고있는데 절차형으로 프로그래밍하려니 어렵다"

## Keywords
- Observable, RxJava, Reactor Sodium
- Spring 5 MVC, AKKA-http, Vert.x, Playframework
- Reactive-streams

## Backpressure?
*주: 정확히 어떤 논조에서 나온 토픽인지 기억이 잘 안남;*

서버 과부하 상태에서 추가로 들어오는 요청을 핸들링하는 기능?

[[Reactive Programming with Spring 5.0 M1](https://spring.io/blog/2016/07/28/reactive-programming-with-spring-5-0-m1)]