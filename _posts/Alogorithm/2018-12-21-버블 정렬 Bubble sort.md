---
title: "버블 정렬 Bubble Sort"
categories: 
  - Algorithm
last_modified_at: 2018-12-21T13:00:00+09:00
tags:
- Algorithm
- Bubble Sort
toc: true
sidebar_main: true
---

## Intro

> - 버블 정렬의 이해



## 버블 정렬 Bubble Sort

버블 정렬은 두 인접한 원소를 검사하여 정렬하는 방법이다. 

시간복잡도가 O(n<sup>2</sup>)로 느리지만, 단순하다. [^1]

[^1]:[위키백과](https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC)


## 예제 

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/bubble/1.png?raw=true)




## 버블 정렬의 시간 복잡도

>비교 횟수

* 최상, 평균, 최악 모두 일정

* n-1, n-2, ... ,2, 1 번 = n(n-1)/2

>교환 횟수

* 역순으로 정렬되어 있는 최악의 경우, 한번 교환시 3번의 이동 필요 = 3n(n-1)/2

* 최상의 경우 이미 정렬되어 있으므로 교환 하지않음


> T(n)=O(n<sup>2</sup>)



## 자바 구현

<script src="https://gist.github.com/lesslate/2473ea9f98f30dfdd94ea27f631b7d16.js"></script>

## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/bubble/2.png?raw=true)



## 참고자료


[Heee's 블로그](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)

