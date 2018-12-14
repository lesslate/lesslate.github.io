---
title: "Predictive 파서"
categories: 
  - Compiler
last_modified_at: 2018-12-14T13:00:00+09:00
tags: 
  - Compiler 
toc: true
sidebar_main: true
---

## Intro

> - Predictive 파서의 이해

## Predictive 파서

Recurisve-descent 파서는 생성 규칙이 바뀔 때마다 구문 분석기를 구현한 프로그램을 다시 고쳐 써야 하는 단점을 갖는다.

이에 비해 predictive 파서는 생성 규칙이 바뀌더라도 구동루틴은 고치지 않고 단지 구문 분석기의 행동을 제어하는
파싱 테이블만 다시 구해서 구문 분석기를 구현 할 수 있는 방법이다.

**Predictive 파서**

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/1.png?raw=true)

### 파싱 테이블

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/2.png?raw=true)


predictive 파서가 사용하는 파싱 테이블을 predictive 파싱 테이블 또는 LL파싱 테이블이라 부른다.

Nontermianl과 Terminal의 2차원 배열 구조로 되어있고, 행과 열이 만나는 부분은 생성 규칙 번호가 채워진다.


Predictive 파싱 테이블의 크기는 항상 ![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/3.png?raw=true)이 된다.

1이 더해지는 이유는 입력의 끝을 나타내는 $이 있기 때문이다.


> 파싱 테이블 예제

```
1. S -> aSb
2. S -> bA
3. A -> aA
4. A -> b
```
**파싱 테이블**

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/4.png?raw=true)

여기서 빈 엔트리는 에러를 나타내며 스택 top이 S이고 입력심벌이 a라면 1번 생성 규칙으로 확장하라는 의미이다.



> 구문 분석 예제

```
1. S -> aS
2. S -> bA
3. A -> d
4. A -> ccA
```

**파싱 테이블**

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/6.png?raw=true)

**predictive 구문 분석**

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/predictiveparser/5.png?raw=true)


## 참고 저서

[오세만, 컴파일러 입문, 정익사,2010, 289쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)

