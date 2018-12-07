---
title: "우선순위 큐 Priority Queue"
categories: 
  - DataStructure
last_modified_at: 2018-12-02T13:00:00+09:00
tags:
- DataStructure
- Priority Queue
- Java
toc: true
sidebar_main: true
---

## Intro

> - 우선 순위큐에 대한 이해



## 우선순위 큐

각 원소들은 우선순위를 갖고있고, 높은 우선순위를 가진 원소가 먼저 처리된다.

같은 우선순위를 가진다면 큐에서 순서에 의해 처리된다.

우선순위 큐는 "리스트"나 "맵"과 같이 추상적인 개념이다.

힙이나 다양한 방법을 이용해 구현될 수 있다.[^1]

[^1]:[위키백과](https://ko.wikipedia.org/wiki/%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84_%ED%81%90)



## 우선순위 큐 구현 방법

* 배열을 통해 구현
* 연결리스트를 통해 구현
* 힙(Heap)을 이용하여 구현

배열이나 연결리스트를 이용해 구현할 경우 간단하게 구현가능하지만

배열로 구현할 경우 데이터 삽입, 삭제과정에서 데이터를 이동하는 연산을 해야하며

삽입위치를 찾기위해 저장된 모든 데이터와 우선순위 비교가 필요해지는 단점이있다.

연결리스트 또한 삽입 위치를 찾기위해 마지막 노드까지 데이터와 우선순위를 비교할 수있다.

결국 데이터량이 많아질수록 비교량이 많아지므로 성능이 저하된다.

그렇기 때문에 주로 우선순위 큐는 ``힙(Heap)``을 이용해서 구현한다.[^2]

[^2]:[참고블로그](http://hannom.tistory.com/36)


## 힙 삽입 삭제 과정

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/1.png?raw=true)

가장 작은 값이 루트에 위치하게되는 최소힙을 예로 들었을때


### 삽입

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/2.png?raw=true)

3을 삽입한다면 마지막 노드에 3을 삽입한 뒤

부모노드 7과 비교한다

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/3.png?raw=true)


3이 우선순위가 높으므로 위치교환

다시 부모노드 4와 비교 후 위치교환

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/4.png?raw=true)

루트노드 2와 비교하지만 우선순위가 낮으므로

3의 위치는 확정된다.

### 삭제

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/5.png?raw=true)

삭제는 가장 높은 우선순위인 루트노드의 값 2를 삭제하고

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/6.png?raw=true)

마지막 노드의 값 7을 루트노드로 옮긴다

![7](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/7.png?raw=true)

자식노드와 비교후 우선순위가 높은 값 3과 7교환

![8](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/8.png?raw=true)

마찬가지로 7과 4 교환

![9](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/9.png?raw=true)

15가 우선순위가 낮으므로 교환하지않는다

## 배열을 이용한 우선순위 큐 JAVA

<script src="https://gist.github.com/lesslate/63a8e53f51cae23a87902668cb4a5f8e.js"></script>

## 실행 결과

![10](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/PriorityQueue/10.png?raw=true)

## 참고자료


