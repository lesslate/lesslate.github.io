---
title: "언리얼4 Blueprint 데미지 표기 (Damage Floating Text)"
categories: 
  - Unreal4
last_modified_at: 2019-04-14T13:00:00+09:00
tags: 
  - unreal4 
  - Blueprint
  - Widget
toc: true
sidebar_main: true
---

## Intro

> - 데미지 표기 위젯

## 블루프린트 위젯 제작


> 디자인

블루프린트 위젯을 생성하고 `Size Box`안에 텍스트 블록을 추가한뒤 알파 값이 0으로 사라지는 애니메이션을 추가한다.

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/damageText/1.gif?raw=true)


> 이벤트 그래프

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/damageText/2.png?raw=true)

Construct 이벤트에서 위젯을 받아온 Vector2D로 띄우고 움직일 방향(Final Location)을 저장하고 텍스트를 받아온 데미지로 설정하고 사라지는 애니메이션을 재생시킨다.
이때 Tick이벤트 에서 저장한 `Final Location`방향으로 위젯을 이동하도록 한다.

애니메이션이 끝나면 위젯을 제거한다. 

`SetText`의 타겟인 `DamageText` 블록은 디테일창에서 변수인지에 체크해주면 변수로 사용할 수 있다.

`DamageToDisplay`와 `InitialScreenLocation` 변수는 데미지를 입은 액터로부터 받아와야하기 때문에 `인스턴스 편집가능`과 `스폰시 노출`에 체크해준다.

> 헤드샷 위젯 복사

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/damageText/3.png?raw=true)

헤드샷 데미지를 표기할 위젯을 따로 사용하기위해 위젯을 복사하고 텍스트를 수정한다.

## 위젯 생성하기

몬스터의 이벤트그래프에서 `AnyDamage` 이벤트를 통해 데미지를 받으면 헤드샷 판정여부에 따라 다른 위젯을 띄우며

액터의 위치와 받은 데미지를 생성될 위젯에 전달해준다.

헤드샷 여부는 C++ 코드에서 받아올수 있다.

```cpp
if (BoneName == TEXT("Head"))
	{
		IsHead = true;
	}
```


## 실행 결과

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/damageText/44.gif?raw=true)

## 참고문서

[https://youtu.be/cI77UWsSlLM](https://youtu.be/cI77UWsSlLM)