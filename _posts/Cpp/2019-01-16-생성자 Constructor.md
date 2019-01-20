---
title: "생성자 Constructor"
categories: 
  - Cpp
last_modified_at: 2019-01-16T13:00:00+09:00
tags: 
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 생성자 Constructor의 이해

## 생성자란?

C++ 객체를 생성할 때 객체를 초기화할 수 있다. 클래스는 객체가 생성될 때 자동으로 실행되는 생성자라는 특별한 멤버 함수를 통해 객체를 초기화 한다.

한 클래스에 여러 개의 생성자를 둘 수 있으나, 이 중 하나만 실행 된다.


## 생성자의 특징

* 생성자의 목적

객체가 생성될 때 필요한 초기 작업을 위함이다.



* 생성자는 한번만 실행

객체가 생성되는 시점에 한번만 자동으로 실행된다.



* 생성자 함수의 이름은 클래스와 동일해야함

이로 인해 생성자는 다른 멤버 함수와 쉽게 구분가능.



* 생성자 함수 원형에 리턴 타입을 선언하지 않음

생성자는 함수이지만 리턴 타입을 선언하면 오류가 발생한다.



* 생성자는 중복 가능하다.

한 클래스에 여러 개 의 생성자는 만들 수 있다.

매개 변수 개수나 타입이 서로 다르게 선언되어야 함
```
ex) 
Circle();
Circle(int r);
```

## 예제 코드

**2개의 생성자를 가진 Circle 클래스**

<script src="https://gist.github.com/lesslate/2339921bcdbeeec359827663d7060b22.js"></script>


**객체가 생성되는 과정과 생성자 실행**

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/constructor/1.png?raw=true)


**디폴트 값이 정해진 생성자**

<script src="https://gist.github.com/lesslate/95b580ffca8e16b82e906505fc6f48c0.js"></script>

실행결과

```
0 0
100 0
100 200
```


## 참고 자료

[황기태, 명품 C++ Programming, 생능출판사,2013, 105쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=7275362)

![Wikidocs](https://wikidocs.net/17145)