---
title: "연결 리스트 Linked List"
categories: 
  - DataStructure
last_modified_at: 2019-04-23T13:00:00+09:00
tags:
- DataStructure
- Linked List
toc: true
sidebar_main: true
---

## Intro

> - 연결 리스트에 대한 이해



## 연결리스트 (Linked List)

데이터를 저장할 때 데이터와 포인터를 이용해 한 줄로 연결되어 있는 방식으로 저장하는 자료 구조이다.

노드의 중간 지점에서도 자료를 삽입 삭제(O(1))를 쉽게 할 수 있지만 특정 노드를 검색(O(n))하기 어려운 단점이있다.

## 단일 연결 리스트

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/rinkedList/1.png?raw=true)

노드 추가, 삭제가 용이하며 마지막 노드를 찾으려면 끝까지 찾아가야하기 때문에 O(n)으로 느리다.

노드 추가시 메모리 동적할당을 이용하므로 공간 낭비가 없다.


## 이중 연결 리스트

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/rinkedList/2.png?raw=true)

양방향으로 연결된 리스트이므로 노드 탐색을 양쪽으로 가능하다. 뒤로도 탐색이 가능하므로 단일 연결리스트에 비해 탐색이 빠를수 있다. 대신 구현이 복잡해지고 메모리를 더 사용하게된다.


## 원형 연결 리스트

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/rinkedList/3.png?raw=true)

리스트의 마지막 노드가 첫번째 노드를 가리키는 리스트이다. 



## 참고자료

[https://opentutorials.org/module/1335/8940](https://opentutorials.org/module/1335/8940)

