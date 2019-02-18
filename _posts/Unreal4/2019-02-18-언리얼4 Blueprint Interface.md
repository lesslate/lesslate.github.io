---
title: "언리얼4 C++ Blueprint Interface"
categories: 
  - Unreal4
last_modified_at: 2019-02-18T13:00:00+09:00
tags: 
  - unreal4 
  - Blueprint
toc: true
sidebar_main: true
---

## Intro

> - 블루프린트 인터페이스 사용

## 블루프린트 인터페이스

``블루프린트 인터페이스``를 사용하면 공통된 방법으로 특정 함수성을 모두 공유하는 다수의 오브젝트 유형과 상호작용 할 수 있다.[^1]

[^1]:[http://api.unrealengine.com/KOR/Engine/Blueprints/UserGuide/Types/Interface/UsingInterfaces/](http://api.unrealengine.com/KOR/Engine/Blueprints/UserGuide/Types/Interface/UsingInterfaces/)

## 예제

블루프린트 인터페이스 생성

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/1.png?raw=true)


사용할 함수 추가


![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/2.png?raw=true)


사용할 블루프린트에 인터페이스 추가(클래스 디폴트)

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/5.png?raw=true)


함수 호출 (LineTrace의 HitResult가 타겟이 되도록함)

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/3.png?raw=true)

> 각기 다른 이벤트 설정

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/4.png?raw=true)

Door_BP에서는 문을 열거나 닫을 수 있고

![7](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/7.png?raw=true)

Lamp_BP에서는 `램프`라는 메시지 출력




## 결과

같은 이벤트를 호출하지만 다른 결과가 나타난다

![7](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/7.gif?raw=true)


![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/6.png?raw=true)


## 레벨 안 블루프린트 지정하기

레벨 안에 존재하는 블루프린트를 지정하기 위해서는

'Actor' 유형 퍼블릭 변수를 만든다음

![8](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/9.png?raw=true)

레벨 에디터의 디테일 탭에서 적합한 블루프린트를 할당해주면

![9](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/8.png?raw=true)

변수로 사용할 수 있다.

![10](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/interface/10.png?raw=true)

## 참고문서

[http://api.unrealengine.com/KOR/Programming/UnrealArchitecture/Reference/Interfaces/](http://api.unrealengine.com/KOR/Programming/UnrealArchitecture/Reference/Interfaces/)

