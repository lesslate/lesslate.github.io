---
title: "동적 계획법 Dynamic Programming"
categories: 
  - Algorithm
last_modified_at: 2018-11-10T13:00:00+09:00
tags:
- Algorithm
- Dynamic Programming
toc: true
sidebar_main: true
---

## Intro

> - 피보나치 수열을 통한 동적 계획법 이해하기



## 동적 계획법

복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법.


## 과정

문제를 여러 개의 하위문제(subproblem)으로 나누어 푼 다음 결합하여 최종 해에 도달.

하위 문제의 해를 저장한뒤 같은 하위 문제가 나올경우 간단하게 해결할 수 있다.

이러한 방법은 계산 횟수를 획기적으로 줄일 수 있다.


## 예제

### 재귀함수 형태의 피보나치 수열
<script src="https://gist.github.com/lesslate/6cc94993a111ef7fcd2c7348d5a1e792.js"></script>


**문제점**



n이 커질수록 재귀트리가 많이 형성되어 계산 속도를 떨어뜨리며 오버플로우가 발생한다. 

![dp](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/dp/fibo.png?raw=true)

fib(5)호출시 트리

### 동적 계획법 형태의 피보나치 수열

동적 계획법에서는 이전에 계산했던 값들을 배열에 저장해 중복계산을 막는다. 

큰 문제에서 작은 문제로 분할해나가는 ``Top-down`` 방식과

작은 문제를 쌓아 큰문제를 푸는 ``Bottom-up``방식이 있다.


#### Top-down 방식

<script src="https://gist.github.com/lesslate/a6b0be2145c5a3ba360f883577ee40d3.js"></script>

![dp2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/dp/fibo2.png?raw=true)

중복되는 값은 저장된 값을 통해 계산과정을 줄일수있다.



#### Bottom-up 방식

<script src="https://gist.github.com/lesslate/b87724d67d4baff9af9d44e476a6bf5f.js"></script>


## 참고자료


[위키백과](https://ko.wikipedia.org/wiki/%EB%8F%99%EC%A0%81_%EA%B3%84%ED%9A%8D%EB%B2%95)

