# **비동기 어플리케이션과 모니터링으로 밀당하기** by **이건희**님
*비동기 어플리케이션을 디버깅 하기 위한 실습기.*

*실제 연사분이 겪으셨던 비동기 코드에 대한 코드에 대한 경험담도 재미있게 풀어주시고*

*BCI 등에 대한 개념도 잘 설명해주셔서 흥미롭고 재미있는 세션이었음.*

## APM이란?
Application performance management

성능 메트릭 + 원인을 찾기 위한 Alpha

## BCI
Byte code instumentation

bytecode에 직접 수정을 가하는 방식

## 어떻게 구현되는가? `premain()`
- main() 전에 수행됨
- transform을 통한 class 생성도 가능
- ASM 등의 툴

## 비동기적 어플리케이션 디버깅의 실상
*연결고리가 없는 쓰레드 간의 연결고리를 나타내기 위한 삽질기*

## 비동기 Application 모니터링의 목표!
- 비동기이든 동기이든 동일한 view를 제공
- InheritableThreadLocal