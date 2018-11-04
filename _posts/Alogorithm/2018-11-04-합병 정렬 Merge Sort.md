---
title: "합병정렬 Merge Sort"
categories: 
  - Algorithm
last_modified_at: 2018-11-04T13:00:00+09:00
tags:
- Algorithm
- Java
- Merge Sort
toc: true
---

## Intro

합병 정렬을 이해하고 구현해보기



## 합병정렬 (Merge Sort)

합병정렬은 비교 기반 정렬 알고리즘이며 안정 정렬에 속한다.

분할 정복 알고리즘중 하나이다.



## 합병정렬 연산과정

![merge](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/merge/merger.png?raw=true)

리스트길이가 0또는 1이 될때까지 리스트를 절반으로 잘라 두 부분으로 나누고

각 부분 리스트를 재귀적으로 합병 정렬한다.

다시 하나의 리스트로 합병한다.



## 합병과정

![merge2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/merge/merge2.png?raw=true)

2개 리스트 값들을 하나씩 비교하며 둘중 더작은 값을 새로운 리스트에 넣는다.

두 개의 리스트중 하나가 비게되면 다른 리스트의 값을 모두 새로운 리스트에 넣는다.

새로운 만들어진 리스트를 원래 리스트로 복사




## 합병 정렬의 장단점

*장점
 * 안정적인 정렬
  * 입력 데이터가 무엇이든 정렬시간은 (O(nlog<sub>2</sub><sup>n</sup>)으로 동일)
 * 레코드를 연결리스트로 구성하면 링크 인덱스만 변경되므로 데이터 이동은 아주 작아진다.
  * 제자리 정렬로 구현할 수 있다.
 * 크기가 큰 레코드를 정렬할 경우 연결 리스트를 사용하면, 합병정렬은 어떤 정렬보다도 효율적이다.

*단점
 - 레코드를 배열로 구성하면 임시배열이 필요하다.
 + 제자리정렬이 아니다.
 - 레코드들의 크기가 큰 경우 이동 횟수가 많으므로 많은 시간을 낭비한다
    

## 시간복잡도

분할시 매번 반씩 감소하므로 log<sub>2</sub><sup>N</sup>만큼 반복해야 크기가 1인 배열로 분할된다.

분할시 합병도 진행 하므로 시간복잡도는 O(Nlog<sub>2</sub><sup>N</sup>)이 된다.

합병 정렬은 최악의 경우에도 O(Nlog<sub>2</sub><sup>N</sup>)의 시간복잡도를 가진다.




## JAVA 소스코드

<script src="https://gist.github.com/lesslate/94f3060398198fb7b1bd81e15ab5bdce.js"></script>


## 실행 결과

![result](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Algorithm/merge/result.png?raw=true)





## 참고자료


[위키백과](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)
[Heee's Development Blog](https://gmlwjd9405.github.io/)