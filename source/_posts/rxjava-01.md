---
date: '2017-12-04 03:16 +0900'
title: '[RxJava] Observable의 종류'
tags:
  - rxjava
  - reactive programming
  - observable
categories:
  - java
  - rxjava
published: true
---
# Observable
Observable에는 Hot Observable, Cold Observable 두 종류로 나눌 수 있다. Cold은 옵저버가 subscribe()를 호출하여 구독하지 않으면 데이터를 발행하지 않는 '게은른(Lazy) 접근법'이다. Hot Obsevable은 구독자 존재 여부와 관계없이 데이터를 발행한다. 따라서 여러 구독자를 고려할 수 있다.
<!-- more -->

## Cold Observable
Cold Observable은 just(), fromIterable() 함수를 호출해도 옵저버가 subscribe() 함수를 호출하여 구독하지 않으면 데이터를 발행하지 않는다. 사용되는 예로는 웹 요청, 데이터베이스 쿼리와 파일 읽기 등이다.

## Hot Observable
Cold Observable과는 다르게 구독자가 Observable이 발행하는 데이터를 모두 수신하는 것을 보장하지 못한다. 구독자가 존재하지 않더라도 발행되며, 구독자는 구독을 시작했을 시점부터의 데이터를 수신할 수 있다. 사용되는 예로는 마우스 이벤트, 키보드 이벤트, 싯템 이벤트, 센서 데이터와 주식 가격 등이 있다. 주로 센서 데이터나 이벤트 입력에 많이 사용되는 것 같다.

# 참조
- RxJava 프로그래밍 : 리액티브 프로그래밍 기초부터 안드로이드까지 한번에

