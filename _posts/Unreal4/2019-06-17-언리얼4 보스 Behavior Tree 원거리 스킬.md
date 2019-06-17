---
title: "언리얼4 보스 Behavior Tree 원거리 스킬 패턴"
categories: 
  - Unreal4
last_modified_at: 2019-06-17T13:00:00+09:00
tags: 
  - unreal4 
  - Behavior Tree
  - Blueprint

toc: true
sidebar_main: true
---

## Intro

> - 몬스터 원거리 스킬 패턴 추가

## 스킬 개요

플레이어가 일정거리 떨어졌을때 머리위에 메테오를 떨어뜨리는 스킬을 사용하도록 구성한다.


## 메테오 액터 생성

> 데칼 머티리얼 생성

![decal](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/decalmeterial.png?raw=true)

메테오가 떨어질 위치를 표시할 데칼을 원형 텍스처파일을 통해 `Deferred Decal` 타입의 머티리얼을 만들어준다.

> Meteor 액터 생성

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/3.png?raw=true)

바닥에 만들어둔 데칼과 폭발 파티클을 배치하고 바닥으로부터 1000높이에 `Sphere Collision`과 그 자식으로 운석 파티클을 넣어준다.

콜리전에 `Simulate Physics`를 체크해 액터가 생성되면 운석이 떨어지는듯한 효과를 주도록한다.

> Meteor 이벤트그래프

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/4.png?raw=true)

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/5.png?raw=true)

액터가 생성되면 운석이 떨어지는 소리를 재생시키고 바닥에 닿게되는 1.7초뒤에 폭발소리와 폭발 파티클 재생과 일정범위에 Radial Damage를 주고 데칼과 파티클을 숨기고 액터에 수명을 주었다.

## 비헤이비어 트리 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/1.png?raw=true)

원거리 패턴 트리 아래에 추가하고 메테오를 생성하는 서비스를 추가한다.

> 메테오 생성 서비스

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/6.png?raw=true)

블랙보드 키를 통해 타겟의 위치를 가져온다음 Z값을 -90 시킨위치(캐릭터의 발)에 메테오 액터클래스를 생성시키도록 한다.

## 실행 결과

![GIF](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/MeteorPattern/GIF.gif?raw=true)

## 참고 자료

[https://youtu.be/44azsxdfiok](https://youtu.be/44azsxdfiok)