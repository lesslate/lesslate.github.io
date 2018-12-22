---
title: "Namespace 사용법"
categories: 
  - Cpp
last_modified_at: 2018-11-08T13:00:00+09:00
tags: 
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 네임스페이스 사용법

## 중복된 이름의 함수

![name](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/name.png?raw=true)

이름이 중복되어 빌드시 오류가 발생한다.


## Namespace 할당


![name2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/name2.png?raw=true)

한개의 함수를 Myspace라는 Namespace에 할당시켜주면

오류가 발생하지않고 하나의 함수만 실행된다.

**실행 결과**

![reuslt](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/resu.png?raw=true)


## Namespcae 호출


![name3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/name3.png?raw=true)


Namespace::함수이름 으로 호출하여 사용할수있다.


**실행결과**

![resu2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/resss.png?raw=true)