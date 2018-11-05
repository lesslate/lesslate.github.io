---
title: "Context-free문법 문법 변환"
categories: 
  - Compiler
last_modified_at: 2018-11-05T13:00:00+09:00
tags: 
  - Compiler 
toc: true
---

## Intro

문법을 효율적인 분석을 위한 형태로 바꾸는 기법들


## 1. 필요 없는 생성 규칙 제거



문장을 생성하는데 적용할 수 없는 생성 규칙들은 제거할 수 있다.


### 방법1 Terminating nonterminal 을 구하는 방법


**Terminating nonterminal**

어떤 nonterminal 심벌이 terminal 스트링을 유도할 수 있을 때,
``terminating nonterminal``이라 한다.



**예제**

P={S->A, S->B, B->a}에서 ``terminating nonterminal``을 구해보자

V<sub>N</sub><sup>'</sup>은 생성 규칙의 오른쪽이 모두 terminal만으로 이루어진
생성규칙의 lhs이므로 B와 S를 가지게 된다.

V<sub>N</sub><sup>'</sup>={B,S}

따라서 V<sub>N</sub> - V<sub>N</sub><sup>'</sup> = {S,A,B} - {B,S} = {A} 이다. 

그러므로 A를 가진 모든 생성규칙을 제거하면 P' = {S->B, B->a}가 된다.





### 방법2 도달 가능한 심벌을 구하는 방법



**예제**
```
S->aB
A->aB | aC
B->C
C->b
```
일때 

도달 가능한 심벌 V'을 구한다.
```
V' = {S}
V' = {S,a,B}
V' = {S,a,B,C}
V' = {S,a,B,C,b}
```

따라서 도달 불가능한 심벌은

```
V-V'={S,A,B,C,a,b} - {S,a,B,C,b} = {A}
```

이고 도달 불가능한 심벌을 가진 모든 생성규칙을 제거하면

```
P' = {S->aB, B->C, C->b}가 된다.
```


주어진 문법으로부터 필요 없는 생성 규칙을 제거하기 위해서는 위의 방법1을 적용하고 방법2를 적용한다.


### 필요 없는 생성 규칙 제거 - 방법1+방법2



**예제**
```
P = {S->aS, S->A, S->B, A->aA, B->a, C->aa}
```
일 때 

terminal 스트링을 유도할 수 있는 nonterminal(Terminating Nonterminal)은

V<sub>N</sub>-V<sub>N</sub><sup>'</sup> = {B,C,S}가 된다.

따라서 A가 terminal 스트링을 생성할 수 없는 nonterminal 이므로

```P' = {S->aS, S->B, B->a, C->aa}```가 된다. 

다음으로 도달 가능한 심벌을 구하면

```V'={S,a,B}```가 된다. C는 도달 불가능한 심벌이기 때문에

```P'' = {S->aS, S->B, B->a}```가 된다.

P''이 P로부터 구해진 유용한 생성 규칙만으로 이루어진 집합이다.






## 2. ε-생성 규칙 제거

CFG G=(V<sub>N</sub>, V<sub>T</sub>, P, S)가 다음 조건을 가질 때 ε-free라고 한다.

1.  P가 ε-생성 규칙을 갖지 않거나
2.  S하나만이 ε-생성 규칙을 가지며, 다른 생성 규칙의 오른쪽에 S가 나타나지 않아야 한다.



**ε-free 문법으로 바꾸는 과정 예제**

```S -> aSbS | bSaS | ε``` 일때

ε-생성 규칙을 제거한 집합인 ```P' = {S->aSbS|bSaS}```가 되고

ε를 유도할 수 있는 nonterminal의 집한인 V<sub>Nε</sub> = {S}가 된다.

P'에 속하는 생성 규칙의 오른쪽 부분에 S가 있는 경우, S는 ε를 유도할 수 있기때문에

그 생성 규칙에서 S대신 S와 ε가 교대로 대입되어 P'에 추가된다.

따라서 ```S->aSbS는 S->aSbS|abS|aSb|ab가``` 되고 ```S->bSaS는 S->bSaS|baS|bSa|ba```가 된다.

그래서 P'는 ```S->aSbS|abS|aSb|ab|bSaS|baS|bSa|ba```가 된다. 

시작 심벌이 V<sub>Nε</sub>에 속하므로 ε를 포함하기 때문에 생성규칙 ```S'->S|ε```를 추가한다.

결국 ε-free하게 변환된 생성규칙은 다음과 같다.
```
S'->S|ε
S->aSbS|abS|aSb|ab|bSaS|baS|bSa|ba
```





## 3. 단일 생성 규칙의 제거

생성 규칙의 형태가 A->B와 같이 생성 규칙의 오른쪽에 한 개의 nontermianl만

나오는 생성 규칙을 단일 생성 규칙이라 하며, 불필요한 유도과정이 추가되어 파싱 속도가 느려진다.

따라서 효율적 파싱을 위해 제거하는 것이 바람직하다.



**단일 생성 규칙 제거 방법**

단일 생성 규칙을 모두 제거하여 P'을 구한다. 그리고 각 nonterminal에 대하여
A로부터 단일 생성 규칙을 적용해서 갈 수 있는 nonterminal 집합 V<sub>NA</sub>를 구한다.

V<sub>NA</sub>에 속하는 nonterminal B가 B->a 형태의 생성 규칙이 있다면
A에서 직접 유도 될 수 있도록 A->a를 추가한다.




**예제**
```
E -> E+T | T
T -> T*F | F
F -> (E) | a
```
P'은 단일 생성 규칙을 모두 제거한 것으로 다음과 같다.

```P' = {E->E+T, T->T*F, F->(E), F->a}```

그리고 각 nontermianl에 대하여 다음을 반복한다.

첫 번째로 E에 대하여 V<sub>NE</sub>={T,F}가 된다.

V<sub>NE</sub>에 속하는 nonterminal의 생성 규칙중 단일 생성 규칙이 

아닌 생성 규칙의 rhs를 E에 대한 생성 규칙으로 만든후 P'에 추가하면

다음과 같다.

```P'={E->E+T|T*F|(E)|a, T->T*F, F->(E), F->a}```

두 번째로 V<sub>NT</sub>={F}가 된다. 마찬가지로 적용하면

```P'={E->E+T|T*F|(E)|a, T->T*F|(E)|a, F->(E),F->a}```

마지막으로 V<sub>NF</sub>=ø 이므로 추가되는 생성 규칙이 없다.

결국 단일 생성 규칙을 제거한 문법은 다음과 같다.
```
E -> E+T | T*F | (E) | a
T -> T*F | (E) | a
F -> (E) | a
```




단위 생성 규칙을 제거한 문법을 유도트리로 만들어보면 다음과 같다.


![udo](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/contextfree/udo1.png?raw=true)


![ud](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/compiler/contextfree/udo.png?raw=true)


유도 과정이 많이 짧아진 것을 알수있다.


## 참고 문헌

[컴파일러 입문 - 오세만 저](https://book.naver.com/bookdb/book_detail.nhn?bid=6324381)