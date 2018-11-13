---
title: "퀵정렬 Quick Sort"
categories: 
  - Algorithm
last_modified_at: 2018-11-01T13:00:00+09:00
tags:
- Algorithm
- Java
- QuickSort
toc: true
sidebar_main: true
---

## Intro

퀵 정렬 알고리즘을 이해하고 구현해보기


## 퀵정렬(Quick Sort)

퀵 정렬은 다른 원소와의 비교만으로 정렬을 수행하는 비교정렬에 속한다.

n개의 데이터를 정렬할떄 최악의 경우는 O(n^2) 최선과 평균의 경우 O(nlog2n)이며

다른 정렬에 비교해서 빠른편이다.

퀵정렬은 분할 정복 알고리즘중 하나이며 

분할 정복은 문제를 작은 문제로 분리하여 각각 해결한다음 원래의 문제를 해결하는 방법이다.


## 퀵 정렬 연산과정

![quick](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/quick/Qucik.png?raw=true)



## JAVA 소스코드

<script src="https://gist.github.com/lesslate/5ac1cb11feea77c5150b508c594b81c5.js"></script>





## 실행 결과


![result](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/quick/quick2.png?raw=true)





## 참고자료


[위키백과](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC)