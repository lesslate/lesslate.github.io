---
title: "구문 분석 Left-factoring"
categories: 
  - Compiler
last_modified_at: 2018-11-19T13:00:00+09:00
tags: 
  - Compiler
toc: true
sidebar_main: true
---

## Intro

> - Left-factoring 



## left-factoring 이란

Top-down 구문 분석에서 같은 심벌들을 prefix로 갖는 두개 이상의 생성 규칙이 있을때,

구문 분석기가 어떤 생성 규칙을 적용해야 할지 결정할 수 없다.

따라서 구문 분석 결정 과정을 다음 심벌을 볼 때까지 연기함으로써 혼란을 막을 수 있다.

이 때 공통 앞부분을 새로운 nonterminal을 도입하여 인수 분해한다.

```
A -> αβ | αγ 

<=> A -> α(β | γ) 

<=> A-> αA'
    A' -> β | γ
```
이와 같은 과정을 left-factoring이라 부른다.

**예시**

```
S -> iCtS | ictSeS | a
C -> b
```

공통 앞부분을 인수분해한다.``S -> iCtS(ε|eS)``

``ε|eS``를 새로운 nonterminal S'로 대치하면

```
S -> iCtSS' | a
S' -> eS | ε
C -> b
```

가 된다.




## 참고 저서

[오세만, 컴파일러 입문, 정익사,2010, 253쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)