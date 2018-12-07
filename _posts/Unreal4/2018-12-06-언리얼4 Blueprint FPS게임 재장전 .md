---
title: "언리얼4 Blueprint FPS게임 재장전"
categories: 
  - Unreal4
last_modified_at: 2018-12-07T13:00:00+09:00
tags: 
  - unreal4 
  - Blueprint
toc: true
sidebar_main: true
---

## Intro

> - 총기 재장전과 위젯 블루프린트


## 재장전

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/1.png?raw=true)

플레이어 블루프린트 이벤트 그래프에서 Int형 변수 Ammo와 Remain Ammo를 생성하고

R키를 눌렀을때 현재 Ammo가 30이 아니고 Remain Ammo가 0이 아닐경우에 준비된 애니메이션을 재생시키도록 함


## 몽타주 생성과 노티파이

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/2.png?raw=true)

재장전 애니메이션 몽타주를 생성한뒤

일정한 구간에 재장전 사운드 노티파이를 추가하고

장전이 끝난지점에는 ReloadEnd라는 커스텀 노티파이를 추가했다.


## 애니메이션 이벤트그래프

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/3.png?raw=true)

애니메이션 이벤트 그래프에서 ReloadEnd 노티파이가 실행되면 Player에서 Reload 이벤트가 발생하도록 했다.

## Reload 이벤트

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/4.png?raw=true)

커스텀 이벤트 Reload를 만들고 노티파이에 의해 실행되면

남은 총알의 개수가 장전해야 할 총알 개수보다 작으면 True 크면 False로 수행

```
True 일때

현재 Ammo와 Remain Ammo를 더하고
현재 Ammo로 Set 해준뒤 Remain Ammo는 0으로 Set
```

```

False 일때

Remain Ammo의 값에 장전해야할 Ammo값(30-Ammo)을 빼고
Ammo에는 그만큼 추가해서 Set
```

## 총알 수 표시 위젯

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/5.png?raw=true)

위젯 블루프린트에서 표시될 현재 장전된 총알수와 가진 총알수 Text 위젯 생성

![7](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/7.png?raw=true)

디테일 창에서 바인딩 생성 

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/6.png?raw=true)

Player 블루프린트에서 Ammo와 Remain Ammo의 값을 받아와서 출력하게함


## Blueprint 예시

<iframe height="400" width="650" marginWidth="10" marginHeight="10" src="https://blueprintue.com/render/tpam8ntu" scrolling="no"></iframe>


## 실행결과

![gif](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/reload/GIF.gif?raw=true)


## 참고문서

애니메이션 출처

[Free 3D](https://free3d.com/3d-model/hk416-with-animation-37927.html)