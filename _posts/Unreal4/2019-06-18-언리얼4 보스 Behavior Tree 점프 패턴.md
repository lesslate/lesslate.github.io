---
title: "언리얼4 보스 Behavior Tree 점프 패턴"
categories: 
  - Unreal4
last_modified_at: 2019-06-18T13:00:00+09:00
tags: 
  - unreal4 
  - Behavior Tree
  - Blueprint

toc: true
sidebar_main: true
---

## Intro

> - 몬스터 점프 패턴 추가

## 패턴 개요

플레이어와 거리를 벌리기위해 뒤로 점프하는 패턴 구현

## 비헤이비어 트리 추가

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/BackJump/2.png?raw=true)

점프하는 애니메이션을 재생하는 테스크와 뒤로 점프시키게할 서비스 추가

> 점프 서비스

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/BackJump/1.png?raw=true)

몬스터의 `Forward Vector`를 구한다음 반대쪽 벡터를 곱해준다음 Z값을 300더해 뒤로 Launch 시키도록 했다.

`Add Impulse` 나 `Add Force`보다 `Launch Character` 함수를 사용하여 좀더 자연스럽게 점프시킬수 있었다.

## 실행 결과

![GIF](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/BackJump/GIF.gif?raw=true)

## 참고 자료

[https://youtu.be/l72AjNFnC-c](https://youtu.be/l72AjNFnC-c)