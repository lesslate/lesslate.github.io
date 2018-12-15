---
title: "Predictive 파싱 테이블 구성방법"
categories: 
  - Compiler
last_modified_at: 2018-12-15T13:00:00+09:00
tags: 
  - Compiler 
toc: true
sidebar_main: true
---

## Intro

> - Predictive 파싱테이블 구성방법

## 파싱테이블 구성과 구문분석 과정 예제

```
S -> aA | abA
A -> Ab | a
```

> LL(1) 문법으로 수정

**공통 부분 인수 분해**
```
S -> aA | abA => S -> a(A | bA ) => S -> aS'
                                    S'-> A | bA
```

**left-recursion 제거**

```
A -> aA'
A'-> bA' | ε
```

**수정된 문법**

```
1. S -> aS'
2. S'-> A
3. S'-> bA
4. A -> aA'
5. A'-> bA'
6. A'-> ε
```

> FIRST와 FOLLOW 구하기

```
FIRST(S) = {a}     FOLLOW(S) = {$}
FIRST(A) = {a}     FOLLOW(A) = {$}
FIRST(S')= {a, b}  FOLLOW(S')= {$}
FIRST(A')= {b, ε}  FOLLOW(A')= {$}
```
> 완성된 파싱 테이블

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/PARSING/1.png?raw=true)




>스트링 abab의 구문 분석 과정

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/PARSING/2.png?raw=true)



## 참고 저서

[오세만, 컴파일러 입문, 정익사,2010, 298쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)

