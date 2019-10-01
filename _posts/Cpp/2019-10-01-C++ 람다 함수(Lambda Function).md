---
title: "C++ 람다 함수(Lambda Function)"
categories: 
  - Cpp
last_modified_at: 2019-10-01T13:00:00+09:00
tags: 
  - C++
  - Lambda
toc: true
sidebar_main: true
---

## Intro

> 람다 함수 알아보기

## Lambda


람다 함수란 익명 함수로써 간결한 코드, 필요한 정보만을 사용하여 성능 향상을 얻을 수 있다.

> 구성

```cpp
[] (int value) -> void { ... }
```

람다식은 `introducer, parameter, return type`과 함수 부분으로 구성되어있다. 

> Capture

외부의 변수를 사용하려면 [] 안에 캡쳐를 넣어주어야 한다.

[&] - 외부의 모든 변수를 레퍼런스로 가져온다.

[=] - 외부의 모든 변수를 값으로 가져온다.

[x, &y] - 특정 변수나 참조형으로도 가능하다.

[=, &x] - 모든 변수를 값으로 가져오고 x만 레퍼런스로 가져온다.

[this] - 현재 객체를 가져옴

> mutable

캡쳐한 변수는 내부에 `const`가 붙은 새로운 변수로 복사된다. 그러므로 이 값은 람다함수 내부에서 변경할 수 없게된다. 하지만 `mutable`을 붙이면 외부변수를 복사 할 때 const가 붙지 않게된다. (레퍼런스 캡쳐는 해당하지않음)

## 예시

> 기본 람다식

```cpp
cout << []() -> int {return 1;}()
```

다음과같이 리턴값과 파라메터를 생략 할수도 있다.

```cpp
[]() {cout << "hello"; }();

[]{cout<<"hello2"}();
```



> 벡터와 람다식

```cpp
vector<int> v;
v.push_back(1);
v.push_back(2);

for_each(v.begin(), v.end(), [](int val) {cout << val << endl; });
```


> 캡쳐의 사용

```cpp
int i = 8;
{
  int j = 2;
  [=] { cout << i / j; }();
}
```

= 를 통해 i,j 둘다 사용할 수 있다.


```cpp
[i]() { int j = 2; [=] { cout << i / j; }(); }();
```

바깥 람다에서 i를 캡쳐했기 때문에 사용할 수 있게된다.

> mutable 속성

```cpp
int i = 8;
[i]() mutable
{	
    int j = 2;
	[&, j]() mutable { i /= j; }();
    cout << "복사된 i: " << i;
}();

cout << " 기존 i: " << i;
```

`mutable` 속성을 지정하지않으면 const 지정자가 붙어 연산을 할 수 없게된다.


람다식 내부의 i는 4가 출력되고 기존의 i는 8이 출력된다.