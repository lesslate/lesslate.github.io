---
title: "C++ 스마트 포인터(Smart Pointer)"
categories: 
  - Cpp
last_modified_at: 2019-10-14T13:00:00+09:00
tags: 
  - C++
  - Smart Pointer
toc: true
sidebar_main: true
---

## Intro

> 스마트 포인터 알아보기

## 스마트 포인터

`스마트 포인터`는 C++에서 포인터를 사용할 때 발생하는 여러가지 문제`(Dangling포인터, 메모리 누수 등)`를 줄이기 위해 만들어졌다.

`스마트 포인터`는 포인터처럼 동작하는 클래스 템플릿이며, 사용하지 않는 메모리를 자동으로 해제해준다. 

## 스마트 포인터의 사용법

`스마트포인터`는 <memory> 헤더를 사용하며 , new에서 기본 포인터가 실제 메모리를 가리키도록 초기화한 다음 스마트포인터에 대입하여 사용한다.



## 스마트 포인터의 종류

현재 사용되지않는 `auto_ptr`을 제외하고 현재 사용되는 스마트 포인터의 종류는 다음과 같다.

~~auto_ptr : C++ 11 이후 deprecated~~

1. unique_ptr

2. shared_ptr

3. weak_ptr

## unique_ptr

`unique_ptr`은 하나의 스마트 포인터만이 특정 객체를 소유할 수 있도록 소유권을 가지는 스마트 포인터다.

소유권을 가지고있어야 소멸자가 객체를 삭제할 수 있으며 `move()` 함수를 통해 소유권을 이전할 수있지만 복사할 수 없다.

대입 연산자를 이용한 복사는 오류를 발생시킨다.

> 예제

```cpp
unique_ptr<int> ptr01(new int(5)); // int형 unique_ptr인 ptr01을 선언하고 초기화함.
auto ptr02 = move(ptr01);          // ptr01에서 ptr02로 소유권을 이전함.
// unique_ptr<int> ptr03 = ptr01;  // 대입 연산자를 이용한 복사는 오류를 발생시킴. 
```

C++14 이후 제공되는 `make_unique()` 함수를 사용하면 좀더 `unique_ptr` 인스턴스를 안전하게 생성할 수 있다.

> unique_ptr 사용 예제

```cpp
#include <iostream>
#include <memory>
#include <string>

using namespace std;

class Monster
{

private:
	string name_;
	float hp_;
	float damage_;

public:
	Monster(const string& name, float hp, float damage); // 생성자 선언

	~Monster() { cout << "메모리가 해제되었습니다." << endl; }
	void PrintMonsterInfo();

};

Monster::Monster(const string& name, float hp, float damage) // 생성자 정의

{
	name_ = name;
	hp_ = hp;
	damage_ = damage;

	cout << "생성자 호출" << endl;

}

void Monster::PrintMonsterInfo()
{
	cout << "몬스터 이름 : " << name_ << endl;
	cout << "체력 : " << hp_ << endl;
	cout << "공격력 : " << damage_ << endl;
}
int main()
{
	unique_ptr<Monster> goblin = make_unique<Monster>("고블린", 100.f, 20.f);

	goblin->PrintMonsterInfo();

	return 0;
}
```

`unique_ptr`을 통해 몬스터 객체를 생성하고 정보를 출력한다. 따로 `delete` 하지않아도 메모리가 해제된다. 


## shared_ptr

`shared_ptr`은 하나의 특정 객체를 참조하는 스마트 포인터가 몇개 인지 참조하는 스마트 포인터이다.

참조가 늘어나면 참조 횟수(reference count)가 증가하고 수명이 다하면 감소한다.
이때 `reference count`가 0이되면 메모리를 자동으로 해제한다.

> 예제

```cpp
shared_ptr<int> ptr1(new int(5));
cout << ptr1.use_count() << endl; // 1
auto ptr2(ptr1);
cout << ptr1.use_count() << endl; // 2
auto ptr3 = ptr1;
cout << ptr1.use_count() << endl; // 3
```

`use_count()` 멤버 함수는 `share_ptr` 객체가 가리키고 있는 리소스를 참조중인 소유자 숫자를 리턴한다.

`share_ptr`도 마찬가지로 `make_shared()` 함수를 통해 안전하게 인스턴스를 생성할 수 있다.

> 예제

```cpp
shared_ptr<Monster> dragon = make_shared<Monster>("드래곤", 5000.f, 500.f);

cout << "현재 소유자 수 : " << dragon.use_count() << endl; // 1
auto dragon2 = dragon;
cout << "현재 소유자 수 : " << dragon.use_count() << endl; // 2

dragon2->PrintMonsterInfo();
cout << "메모리 해제" << endl;
dragon2.reset(); // dragon2 해제
	
cout << "현재 소유자 수 : " << dragon.use_count() << endl; // 1
```    

## weak_ptr

`weak_ptr`은 `shared_ptr` 인스턴스가 소유한 객체에 대한 접근을 할 수 있지만 , `Reference Count`가 증가하지 않는 스마트 포인터이다.

`weak_ptr`을 사용하는 이유는 `shared_ptr`이 서로 상대방을 가르키게 된다면 참조횟수가 0이 되지않아 메모리가 해제되지않는(순환참조 circular reference)가 발생하게된다.
이런 순환 참조를 제거하기 위해 `weak_ptr`를 활용한다.

## 참고 자료

[http://tcpschool.com/cpp/cpp_template_smartPointer](http://tcpschool.com/cpp/cpp_template_smartPointer) 