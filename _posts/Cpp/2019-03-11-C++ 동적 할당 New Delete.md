---
title: "C++ 동적 메모리 할당 new delete"
categories: 
  - Cpp
last_modified_at: 2019-03-11T13:00:00+09:00
tags: 
  - C++
  - DynamicMemoryAllocation
toc: true
sidebar_main: true
---

## Intro

> 동적 메모리 할당


## 동적 메모리 할당 및 반환

프로그램 실행중 필요한 만큼의 메모리를 할당받고 반환하는 메커니즘

C언어 에서는 malloc()/free()를 사용하고 C++에서는 new와 delete를 사용한다.

new연산자는 힙에 메모리를 할당받고, delete는 다시 힙으로 메모리를 반환한다.




## 예제

**기본 형식**
```cpp
데이터타입 *포인터변수 = new 데이터타입;
delete 포인터변수;
```

`new` 연산자는 `데이터타입` 크기만큼 힙으로부터 메모리를 할당 받고 주소를 리턴한다.

`포인터변수`는 할당받은 메모리 주소를 가진다.

이때 `데이터타입`은 기본타입 뿐만아니라 struct, class도 포함한다.


>int타입의 동적 할당 , 반환
<script src="https://gist.github.com/lesslate/832325788f1cca9bb11b0440beb45a58.js"></script>

![alo](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/cpp/allocate.png?raw=true)

* delete 로 메모리 반납 후에도 포인터 주소는 메모리를 가리킨다.

따라서 delete 후에 다음과 nullptr을 넣음으로써 좀더 안전한 코딩이 가능하다.

```cpp
ptr = nullptr;

if(nullptr != ptr)
{
    ...
}
```

>배열 할당
<script src="https://gist.github.com/lesslate/3f6f196094f9a7d9c6a6ed1b7aa8342b.js"></script>


>객체의 동적 생성 및 반환
<script src="https://gist.github.com/lesslate/74ee1403fe15bc9839afc1cea074103f.js"></script>

## 참고 자료

[황기태, 명품 C++ Programming, 생능출판사,2013, 163쪽](https://book.naver.com/bookdb/book_detail.nhn?bid=7275362)