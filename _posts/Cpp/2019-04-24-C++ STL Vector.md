---
title: "C++ STL Vector"
categories: 
  - Cpp
last_modified_at: 2019-04-24T13:00:00+09:00
tags: 
  - C++
  - STL
  - Vector
toc: true
sidebar_main: true
---

## Intro

> STL Vector의 이해


## 벡터 (Vector)

벡터는 `시퀀스 컨테이너`중 하나이며, 동적 배열을 C++로 구현한 것이고 자동으로 배열 크기조절과 객체 추가 삭제가 가능하다. [^1]:[위키백과](https://ko.wikipedia.org/wiki/%EB%B2%A1%ED%84%B0_(STL)) 

## 벡터의 선언

```cpp
vector<Data Type> [변수이름]
```

## 벡터 생성자

* vector<T> v : 비어 있는 컨테이너 생성
    
* vector<T> v(n) : 기본값으로 초기화된 n개의 원소를 가지는 vector 생성
    
* vector<T> v(n,m) : m으로 초기화된 n개의 원소를 가지는 vector 생성

* vector<T> v(v2) : v는 vector v2를 복사해서 생성
    


## 벡터의 멤버 함수

* v.assign(n,m); : m의 값으로 n개 원소를 할당

* v.assign(b,e); : 반복자 구간을 b,e로 할당

* v.reserver(n); : n개의 원소를 저장할 공간을 예약

* v.front(); : 첫 번째 원소 참조

* v.back(); : 마지막 원소 참소

* v.clear(); : 모든 원소를 제거 (메모리는 존재)

* v.push_back(n); : 마지막 원소 뒤에 n 삽입

* v.pop_back(); : 마지막 원소 제거

* v.capacity(); : v에 할당된 크기

* v.empty(); : v가 비었는지 조사

* v.begin(); : 첫 원소를 가리키는 반복자

* v.end(); : 마지막 원소를 가리키는 반복자

* v.size(); : v의 원소 갯수

* v.swap(v2) : v2와 v를 swap

* v.resize(n) : 크기를 n으로 변경

* v.insert(n,m,x) : n의 위치에 m개의 x값 삽입

* v.max_size(); : 담을수 있는 최대 원소 갯수

* v.at(n); : n 번째 원소를 참조 (v[n]보다 느리지만 안전)

* v[n]; : n 번쨰 원소 참조

## 예제

<script src="https://gist.github.com/lesslate/a5f9bc6aafe314e2c0aded446e9c9bd8.js"></script>

## 실행 결과

```
7개의 공간을 가지고 원소가 5개 있는 vector 생성
1
2
3
4
5

size : 5 capacity : 7

-----resize(10,1)-----
1
2
3
4
5
1
1
1
1
1

size : 10 capacity : 10

-----pop 3번 수행-----
1
2
3
4
5
1
1

size : 7 capacity : 10

-- resize(3) --
1
2
3

size : 3 capacity : 10

-- vector clear() --
Vector v is empty

size : 0 capacity : 10

```


## 참고 자료

[http://www.cplusplus.com/reference/vector/vector/](http://www.cplusplus.com/reference/vector/vector/)

[위키백과](https://ko.wikipedia.org/wiki/%EB%B2%A1%ED%84%B0_(STL))