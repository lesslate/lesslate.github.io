---
title: "구문 분석 Left-recursion"
categories: 
  - Compiler
last_modified_at: 2018-11-05T13:00:00+09:00
tags: 
  - Compiler
toc: true
sidebar_main: true
---

## Intro

Left-recursive한 문법 변환



## left-recursive 문법


left-recursive한 문법이란 어떤 a에 대해 A +=> Aa의 유도 과정이 있는

nonterminal A가 존재 할 경우 top-down 구문 분석시 같은 생성

규칙이 순환적으로 적용되어 무한 루프에 빠지게된다. 

따라서 문법 변환을 통해 left-recursion을 제거해야만 한다.



## 직접 left-recursion

직접 left-recursion 이란 생성 규칙에서 A -> Aa와 같이 

직접적으로 나타나는 경우이며

이를 제거하는 방법은 다음과 같다.

```
A -> Aα | β

    ↓
 
A -> βA'
A' -> αA' | ε
```

**예시**
```
E -> E + T | T
T -> T * F | F
F -> (E) | id

    ↓

E -> TE'
E' -> +TE' | ε
T -> FT'
T' -> *FT' | ε
F -> (E) | id
```

## 간접 left-recursion

간접 left-recursion이란 유도과정을 통해

순환이 발생하는 경우이며 A +=> Aa 형태이다.

제거하는 방법은 일정한 순서로 nonterminal들을 순서화 한다.

간접 순환이 발생하는 생성 규칙을 대입기법을 통해 제거한다.

대입 기법을 통해 간접 left-recursion을 제거하면 반드시

직접 left-recursion이 나타난다.

**예시**

```
S -> Aa | b
A -> Ac | Sd | e
```

A -> Sd에서 S가 A보다 앞섰기 때문에

S-생성 규칙을 모두 대입하면 다음과 같다.

```
A -> Ac | Aad | bd | e
```

그러면 직접 left-recursion이 나타나므로 이것또한 제거한다.

```
A -> bdA' | eA'
A' -> cA' | adA' | ε
```

모두 제거된 생성 규칙은 다음과 같다.

```
S -> Aa | b
A -> bdA' | eA'
A' -> cA' | adA' | ε
```


## 참고 저서

[오세만, 컴파일러 입문, 정익사,2010, 249쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)