---
title: "C++ 가상 함수와 오버라이딩 Virtual Function & Overriding"
categories: 
  - Cpp
last_modified_at: 2019-03-17T13:00:00+09:00
tags: 
  - C++
  - VirtualFunction
  - Overriding
  - Polymorphism
toc: true
sidebar_main: true
---

## Intro

> 가상 함수와 오버라이딩의 이해


## 가상 함수와 오버라이딩

가상 함수와 오버라이딩은 상속에 기반을 둔 기술이며 상속을 활용한 
소프트웨어 재사용은 가상함수와 오버라이딩으로 이루어진다.


## 오버라이딩 (Overriding)

`오버라이딩`은 파생 클래스에서 기본 클래스에 작성된 가상 함수를 중복 작성하여,
기본 클래스의 가상 함수대신 사용 되는것이다.

기본 클래스의 포인터든 파생 클래스의 포인터든 가상 함수를 호출하면, 파생 클래스에 `오버라이딩`된 함수가 항상 실행된다.

오버라이딩은 C++의 다형성(Polymorphism) 중 하나이며, `함수 재정의` 라고도한다.

> 오버로딩과 오버라이딩 비교

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/overriding/1.png?raw=true)

오버 로딩은 동등한 호출 기회를 가지는 함수가 둘다 존재하지만 오버라이딩은 Base의 함수는 존재감을 잃고 Derived의 함수만 호출된다.


## 가상 함수 (Virtual Function)

`가상 함수`란 `virtual 키워드`로 선언된 멤버 함수이다. 

virtual은 컴파일러에게 자신에 대한 호출 바인딩을 실행 시간까지 미루도록 지시하는 키워드이다.

가상 함수는 기본클래스나 파생클래스 어디에서나 선언 될 수 있다.

## 예제

<script src="https://gist.github.com/lesslate/782fd1721c30e5453420e6e63fcb16b8.js"></script>

**실행결과**

```
Derived::f() called
Derived::f() called
```

## 오버라이딩의 목적

기본 클래스에 가상 함수를 만드는 목적은 파생 클래스들이 자신의 목적에 맞게 가상 함수를 재정의 하도록 하는 것이다. 

기본 클래스의 `가상함수`는 상속받은 파생 클래스에서 구현해야 할 일종의 `함수 인터페이스`를 제공한다.

가상 함수는 '하나의 인터페이스에 대해 서로 다른 모양의 구현' 이라는 [객체 지향](https://lesslate.github.io/cpp/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/)의 다형성을 실현하는 도구이다.

## 오버라이딩을 이용한 다형성 예시

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/overriding/2.png?raw=true)

기본클래스 Shape에서 가상 함수 draw를 선언 함으로써 인터페이스를 제공하고 각 파생클래스에서 draw 함수를 오버라이딩하여 각자의 기능을 정의 한다.

paint 함수에서 포인터를 통해 p가 가리키는 객체에 오버라이딩된 draw함수를 호출 하도록한다.

이것이 바로 `오버라이딩을 통한 다형성의 실현`이라고 볼 수 있다.

## 참고 자료

[황기태, 명품 C++ Programming, 생능출판사,2013, 418쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=7275362)