---
date: '2017-12-17 21:17 +0900'
published: true 
title: 함수형 프로그래밍이란?
tags:
  - functional programming
  - java
categories:
  - 자바
  - 함수형 프로그래밍
---
함수형 프로그래밍을 쓰고 있었지만, 제대로 쓰고 있는 것인지 의문이 들었다. 좀 더 제대로 공부하고 정리하기 위해 Becoming Functional이라는 책을 읽게 되었다. 이 책을 읽으면서 함수형 프로그래밍을 정

<!-- more -->
# 특징
함수형 프로그래밍은 다음과 같은 특징들이 있다. 특징들을 번역하려고 했지만, 그 중에 너무 어색한 것은 영문으로 그대로 표기했다.
## 1급 함수 (First-class functions)
일반적으로 "1급 시민"은 다음 특징 있다.
* 변수에 담을 수 있다.
* 인자로 전달할 수 있다.
* 반환값(return value)으로 전달할 수 있다.

함수를 "1급 시민"으로 취급할 수 있는데, 다음과 같은 추가적인 조건이 필요하다.
* 런타임 생성이 가능하다.
* 익명으로 생성이 가능하다.

## 순수 함수 (Pure functions)
순수 함수는 주어진 입력으로 계산하는 것 이외에 프로그램의 실행에 영향을 미치지 않아야 하며, 이를 부수 효과(side effect)가 없어야 한다.

## 재귀 (Recursion)
재귀는 알고리즘을 더 간결하게 만들어준다. 그리고 함수의 입력에 따라서만 동작하게 해준다. 우리가 신경써야 할 것은 재귀의 반복이 계속되어야 하는지이다.

## Immutable variables
Immutable variables는 한 번 값을 할당하면, 바뀔 수 없다.

## Nonstrict evaluation
Nonstrict Evaluation은 우리가 아직 계산되지 않은 변수를 가질 수 있게 해준다. 우리가 지금까지 사용했었던 것은 정의되어야 변수를 할당하는 Strict Evaluation이었다. Nonstrict는 우리가 처음 호출되기 전에도 계산되지 않은 상태로 변수를 가질 수 있다는 것이다. 

## 표현법 (Statements)
표현법은 반환값(return value)을 가진 평가가능한 코드 조각이다. If문을 생각하면 이해가 쉽다. 코드의 각 라인은 부수 효과(side effect)가 거의 없는 표현법으로 취급될 수 있다. 

## Pattern matching
패턴 매칭은 수학에서는 볼 수 없지만, 특정 변수의 수를 줄여 함수형 프로그래밍을 도와준다. 코드에서 보통 우리는 객체 안에 변수들을 한데 모아서 캡슐화한다. 패턴 매칭은 타입 체크를 도와주고, 객체로부터 요소들을 뽑아낼 수 있다.
 

# 참고
[JavaScript의 함수는 1급 객체(first class object)이다](https://bestalign.github.io/2015/10/18/first-class-object/)
