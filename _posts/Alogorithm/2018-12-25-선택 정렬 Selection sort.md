---
title: "선택 정렬 Selection Sort"
categories: 
  - Algorithm
last_modified_at: 2018-12-21T13:00:00+09:00
tags:
- Algorithm
- Selection Sort
toc: true
sidebar_main: true
---

## Intro

> - 선택 정렬의 이해



## 선택 정렬 Selection Sort

선택 정렬(Selection Sort)은 제자리 정렬 알고리즘의 하나로, 다음과 같은 순서로 이루어진다.

1.주어진 리스트 중에 최소값을 찾는다.
2.그 값을 맨 앞에 위치한 값과 교체한다(패스(pass)).
3.맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.

n개의 주어진 리스트를 정렬하는 데에는 Θ(n2) 만큼의 시간이 걸린다. [^1]

[^1]:[위키백과](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)


## 예제 

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/SELECTION/1.png?raw=true)




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


[Heee's 블로그](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

