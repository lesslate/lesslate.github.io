---
title: "생성 규칙 LOOKAHEAD"
categories: 
  - Compiler
last_modified_at: 2018-12-13T13:00:00+09:00
tags: 
  - Compiler 
toc: true
sidebar_main: true
---

## Intro

> - LOOKAHEAD의 이해

## LOOKAHEAD

Recursive-descent 파서를 구현할 때 프로시저 작성시 한 생성규칙을 적용했을 때 그 생성 규칙에서 생성할 수 있는 terminal을 알아야하는데 이것을 그 생성 규칙의 ``LOOKAHEAD``라고 한다.


LOOKAHEAD 계산방법

LOOKAHEAD(A -> X<sub>1</sub>X<sub>2</sub>...X<sub>n</sub>)

= FIRST(X<sub>1</sub> ⊕ FIRST(X<sub>2</sub>) ⊕ ... ⊕ FIRST(X<sub>n</sub> ⊕ FOLLOW(A)))

**예제**

다음 문법의 LOOKAHEAD
```
E  -> TE`
E` -> +TE` | ε
T  -> FT`
T` -> *FT` | ε
F  -> (E) | id
```

```
LOOKAHEAD(E -> TE') = FIRST(T) ⊕ FIRST(E') ⊕ FOLLOW(E)

                    = {(, id} ⊕ {+, ε} ⊕ {), $}
                    
                    = {(, id}
                    
LOOKAHEAD(E' -> +TE') = FIRST(+) ⊕ FIRST(T) ⊕ FIRST(E') ⊕ FOLLOW(E')

                    = {+} ⊕ {(,id} ⊕ {+, ε} ⊕ {), $}
                    
                    = {+}
                    
LOOKAHEAD(E' -> ε) = FIRST(ε) ⊕ FOLLOW(E') 
                    
                    = {), $}
                    
LOOKAHEAD(T -> FT') = FIRST(F) ⊕ FIRST(T') ⊕ FOLLOW(T)

                    = {(, id} ⊕ {*, ε} ⊕ {+, ), $}
                    
                    = {(, id}
                    
LOOKAHEAD(T' -> *FT') = FIRST(*) ⊕ FIRST(F) ⊕ FIRST(T') ⊕ FOLLOW(T')

                    = {*} ⊕ {(, id} ⊕ {*, ε} ⊕ {+, ), $}
                    
                    = {*}
                    
LOOKAHEAD(T' -> ε) = FIRST(ε) ⊕ FOLLOW(T')
                    
                    = {+, ), $}

LOOKAHEAD(F -> (E)) = FIRST(() ⊕ FIRST(E) ⊕ FIRST() ⊕ FOLLOW(F)

                    = {(} ⊕ {(,id} ⊕ {(} ⊕ {*, +, ), $}
                    
                    = {(}

LOOKAHEAD(F -> id = FIRST(id) ⊕ FOLLOW(F)

                    = {id} ⊕ {*, +, ), $}
                    
                    = {id}
                    
```
                    



## 참고 저서

[오세만, 컴파일러 입문, 정익사,2010, 281쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)

