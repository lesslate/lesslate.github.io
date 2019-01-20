---
title: "소멸자 Destructor"
categories: 
  - Cpp
last_modified_at: 2019-01-20T13:00:00+09:00
tags: 
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 소멸자

## 소멸자란?

객체가 소멸되면 객체 메모리는 반환되며

객체가 소멸될때 반드시 소멸자 함수가 실행된다.

## 소멸자의 특징

* 소멸자의 목적

객체가 사라질 때 마무리 작업을 위함이다.



* 소멸자의 이름

클래스 이름 앞에 ~를 붙인다.

``ex)Circle::~Circle(){...}``



* 소멸자는 리턴 타입이 없으며 어떤 값도 리턴해서는 안 된다

생성자와 동일하다.



* 소멸자는 오직 한 개만 존재하며 매개 변수를 가지지 않는다.

생성자와 달리 한 개만 존재하며 매개변수를 가지지않음.



* 선언된 소멸자가 없으면 기본 소멸자가 자동으로 생성

생성자와 마찬가지로 컴파일러가 자동으로 생성한다.


## 예제 코드

<script src="https://gist.github.com/lesslate/ed7f5e387f389f49a4cfa5b0aee45aea.js"></script>


실행결과

```
반지름 1원 생성
반지름 30원 생성
반지름 30원 소멸
반지름 1원 소멸
```

함수의 스택에 생성된 pizza, donut 순서로 객체가 소멸된다.


## 참고 자료

[황기태, 명품 C++ Programming, 생능출판사,2013, 114쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=7275362)

![Wikidocs](https://wikidocs.net/17145)