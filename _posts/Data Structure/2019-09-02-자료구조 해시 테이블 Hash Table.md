---
title: "해시 테이블 Hash Table"
categories: 
  - DataStructure
last_modified_at: 2019-09-02T13:00:00+09:00
tags:
- DataStructure
- Hash Table
toc: true
sidebar_main: true
---

## Intro

> - 해시 테이블에 대한 이해



## 해싱

`해싱(Hashing)`이란 데이터를 입력받아 완전 다른 데이터로 바꾸어 놓는 작업이다.


## 해시 테이블

`Hash Function`을 이용하여 임의의 길의의 데이터(키)를 `해싱`하여 그 값(해시 값)을 고정길이 데이터로 사상한다.

해시 함수는 `해시 값`보다 많은 데이터를 해싱하기 때문에 다른 데이터가 같은 해시 값을 가지는 `충돌(Collision)`이 발생 할수 있다.

해시 테이블을 사용하는 이유는 해시 값을 이용해 빠른 검색,삽입,삭제(`O(1)`)가 가능하기 때문이다. 

> 충돌이 많이 일어나게되면 검색시 시간복잡도가 `O(1)`에서 `O(n)`이 될수 있다.

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/HashTable/1.png?raw=true)

## 해싱 충돌 해결 방법

> 폐쇄 주소법(Closed Addressing) 

충돌 발생시 해시 테이블 내부에서 문제를 해결

* Chaining

충돌 발생시 연결 리스트로 데이터를 연결하는 방식이며 데이터 수가 많아지면 효율성이 떨어진다.

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/DataStructure/HashTable/2.png?raw=true)


> 개방 주소법(Open Addressing) 

충돌 발생시 해시 테이블 외부에서 공간을 할당하여 문제를 수습

* 선형 탐사(Linear Probing) : 고정 값 이동 후 다음 빈 버켓을 찾아 데이터를 삽입

* 제곱 탐사(Quadratic Probing) : 제곱만큼 건너뛴 버켓에 데이터 삽입

* 이중 탐사(Double Hasing) : 다른 해시함수를 한번더 적용시켜 삽입



## 참고자료

[https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hashtable](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hashtable)

[https://youtu.be/Vi0hauJemxA](https://youtu.be/Vi0hauJemxA)
