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
Observable 클래스는 데이터의 변화가 발생하는 데이터 소스다. 그리고 디자인 패턴의 옵저버 패턴을 구현한다. 옵저버 패턴은 객체의 상태 변화를 관찰하는 옵저버(관찰자) 목록을 객체에 등록한다. 그 후 상태 변화가 있을 떄마다 메서드를 호출하여 객체가 각 옵저버들에게 변화를 알려준다. RxJava에서는 onNext, onComplete, onError와 같은 메소드로 구독자에게 상태의 변화를 알린다. Observable에는 Hot Observable, Cold Observable 두 종류로 나눌 수 있다. 
<!-- more -->

## Cold Observable
Cold Observable은 just(), fromIterable() 함수를 호출해도 옵저버가 subscribe() 함수를 호출하여 구독하지 않으면 데이터를 발행하지 않는 '게은른(Lazy) 접근법'이다. 사용되는 예로는 웹 요청, 데이터베이스 쿼리와 파일 읽기 등이다.

## Hot Observable
Hot Obsevable은 구독자 존재 여부와 관계없이 데이터를 발행한다. 따라서 여러 구독자를 고려할 수 있다. 하지만 Cold Observable과는 다르게 구독자가 Observable이 발행하는 데이터를 모두 수신하는 것을 보장하지 못한다. 구독자가 존재하지 않더라도 발행되며, 구독자는 구독을 시작했을 시점부터의 데이터를 수신할 수 있다. 사용되는 예로는 마우스 이벤트, 키보드 이벤트, 싯템 이벤트, 센서 데이터와 주식 가격 등이 있다. 주로 센서 데이터나 이벤트 입력에 많이 사용되는 것 같다.

# 참조
- RxJava 프로그래밍 : 리액티브 프로그래밍 기초부터 안드로이드까지 한번에

