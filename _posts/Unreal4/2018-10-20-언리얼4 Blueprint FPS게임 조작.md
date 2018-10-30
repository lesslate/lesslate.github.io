---
title: "언리얼4 Blueprint FPS게임 조작"
categories: 
  - Unreal4
last_modified_at: 2018-10-20T13:00:00+09:00
tags: 
  - unreal4 
  - Blueprint
toc: true
---

## Intro

캐릭터 블루프린트 생성과 FPS게임 조작설정

## 캐릭터로 사용할 블루프린트 생성

![bp](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/blueprint.png?raw=true)

![chra](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/bpcha.png?raw=true)

## 뷰포트 1인칭 설정

사용할 3D 총기 에셋을 임포트합니다

![hk](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/hk416.png?raw=true)

총기 모델 출처
[Free 3D](https://free3d.com/3d-model/hk416-with-animation-37927.html)



![mesh](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/unreal1.png?raw=true)

Mesh아래에 Camera와 Camera아래에 사용할 스켈레탈 메시를 넣어준뒤

카메라앞에 맞춰주었습니다.

![mesh2](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/unreal2.png?raw=true)

## 캐릭터 이동과 카메라제어 Blueprint

Turn 입력 축과 LookUp입력 축을 가져와 카메라를 제어하는 블루프린트

![cam](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/camera.png?raw=true)

MoveForward,MoveRight 입력축을 이용해 캐릭터를 월드상에서 이동할 수 있게하는 블루프린트
(중간에 변수를 저장시켜 애니메이션 블루프린트에서 사용할수있게했습니다.) 

![move](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/Move.png?raw=true)

**점프와 달리기**

Jump키 (Space)가 Pressed 상태일때 캐릭터를 점프시키고 Released 상태일때 점프를 중단하는 블루프린트

왼쪽 Shift키를 누르면 Character Movement의 Walk Speed값을 늘려 이동속도를 빠르게하는 블루프린트
(마찬가지로 변수를 저장시켜 애니메이션 블루프린트에서 활용할수있게했습니다.)

![jump](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/jumpsprint.png?raw=true)




**Blueprint 예시**

<iframe height="400" width="650" marginWidth="10" marginHeight="10" src="https://blueprintue.com/render/6nu6u376" scrolling="no"></iframe>



##실행결과

![Gif](https://github.com/lesslate/blog/blob/master/assets/img/Unreal/GIF.gif?raw=true)