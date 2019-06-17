---
title: "언리얼4 보스 Behavior Tree 몬스터 좌우 판별"
categories: 
  - Unreal4
last_modified_at: 2019-05-30T13:00:00+09:00
tags: 
  - unreal4 
  - Behavior Tree
  - Blueprint
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 몬스터 AI 타겟 좌우 판별

## 좌우 판별하기

> 서비스 생성 후 타겟의 좌우를 판별하는 함수 생성

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Direction/1.png?raw=true)

몬스터에서 타겟으로 향하는 벡터(타겟위치 - 몬스터위치) 와 Forward 벡터를 외적한다음 Up 벡터와 내적하면 그 값이 양수일때 왼쪽 음수일때 오른쪽으로 판별 할 수 있다.


## 방향별 행동 트리 구성

> 출력 값에 따라 블랙보드 번호 지정

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Direction/2.png?raw=true)

일정 값 사이에 있을땐 정면이있다고 판단하여 0번 양수일땐 -1 음수일땐 1번을 블랙보드 키에 저장한다.

> 비헤이비어 트리 구성

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Direction/3.png?raw=true)

이에 따라 서비스 실행후 0번일땐 Wait를 -1일때 왼쪽으로 회전하는 노드 반대로 1일땐 오른쪽으로 회전하는 노드 구성

## 실행 결과

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Direction/GIF.gif?raw=true)

## 참고 자료

[이득우 게임과 여행 블로그](http://blog.dustinlee.me/221411770100)