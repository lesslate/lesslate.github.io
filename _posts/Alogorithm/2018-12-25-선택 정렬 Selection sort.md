---
title: "선택 정렬 Selection Sort"
categories: 
  - Algorithm
last_modified_at: 2018-12-25T13:00:00+09:00
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




## 선택 정렬의 시간복잡도

>비교 횟수

* 두개의 for문 외부 루프 (n-1)번

* 내부 루프(최솟값 찾기) : n-1, n-2, ..., 2, 1번

>교환 횟수

* 외부 루프의 실행 횟수

* 한번 교환시 3번의 이동 3(n-1)


> T(n)=(n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n<sup>2</sup>)

## 선택 정렬의 특징

시간 복잡도 O(n<sup>2</sup>)인 정렬 알고리즘 중에서 선택 정렬은 버블 정렬보다 항상 우수하다

장점 : 자료 이동 횟수가 미리 결정된다. (메모리가 제한적인 경우에 사용시 성능 상의 이점이 있다)

단점 : 안정성을 만족하지 않는다. 값이 같은 레코드가 있는 경우 상대적인 위치가 변경될 수 있다.

## 자바 구현

<script src="https://gist.github.com/lesslate/d6b8a25ba4633660805800d992bf1903.js"></script>

## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/SELECTION/2.png?raw=true)



## 참고자료


[Heee's 블로그](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

