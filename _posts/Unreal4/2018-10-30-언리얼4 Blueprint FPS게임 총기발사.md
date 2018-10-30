---
title: "언리얼4 Blueprint FPS게임 총기발사"
categories: 
  - Unreal4
last_modified_at: 2018-10-30T13:00:00+09:00
tags: 
  - unreal4 
  - Blueprint
toc: true
---

## Intro

애니메이션 블루프린트와 총기발사 블루프린트 만들어보기


## 애니메이션 블루프린트

![animbp](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/bpanim.png?raw=true)

Animation 블루프린트를 만들어 준다음

![state](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/state.png?raw=true)

애님그래프에서 State Machine을 추가했습니다.

![state](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/anim.png?raw=true)

State Machine 내부에 상태를(idle) 정의한뒤

idle 상태의 애니메이션을 넣어주었습니다.

![cache](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/cache.png?raw=true)

다시 애님그래프로 와서 State Machine의 상태를 캐시포즈로 만들어준다음

캐시포즈를 불러와 애니메이션 몽타주를 사용하기위해 슬롯을 만들어 주었습니다.




## 캐릭터 블루프린트 클릭 이벤트 생성

![gate](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/rapid.png?raw=true)


캐릭터 블루프린트 이벤트그래프로 넘어와서

클릭 이벤트 생성후 연속 발사를 위한 Gate를 생성합니다.





## 총기 발사 모션과 사운드 재생

![ammo](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/ammo.png?raw=true)

Int형 변수 ``Ammo`` 생성

![muzzle](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/muzzle.png?raw=true)

![muzzle](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/muzzle2.png?raw=true)

총구화염을 표시하기위해

스켈레톤 파일에서 Silencer 아래에 Muzzle 소켓을 추가한뒤

캐릭터 블루프린트 SkeletalMesh아래에 빈 StaticMesh를 만들고
부모소켓을 Muzzle로 해두었습니다.

![anim](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/montage.png?raw=true)

사용할 모션을 몽타주로 만들어주었습니다.

![fire](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/fire.png?raw=true)

![fire2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/fire2.png?raw=true)

Ammo변수가 0이면 Branch에 의해 딸깍거리는 사운드가 재생되며

0이 아니라면 Ammo변수를 1감소시킨 후 총기 발사 모션과 발사 사운드 재생과

동시에 미리 만들어둔 Muzzle에서 총구 화염을 표시합니다





## Line Trace 활용



![line](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/linetrace.png?raw=true)

LineTraceForObjects를 만들고 Start 부분에는 카메라의 벡터값 

끝나는 위치는 20000만큼 떨어진 지점의 벡터값을 넣어준뒤

LineTrace할 오브젝트 타입 배열을 연결시켜주었습니다.

무시하려는 값은 자신이므로 Self 배열을 넣고 눈으로 확인하기위해

Draw Debug Type을 켜주었습니다.



![line2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Fire/linetrace2.png?raw=true)

LineTrace의 결과값을 분석해 트레이스의 걸린 오브젝트의

Tag값이 Body인경우 Apply Point Damage를 통해

50의 데미지를 주고 피 이펙트가 터지도록 했으며 

그외에 벽,사물 같은 오브젝트는 연기 이펙트가 터지도록 했습니다.



**Blueprint 예시**

<iframe height="400" width="650" marginWidth="10" marginHeight="10" src="https://blueprintue.com/render/repnlw65" scrolling="no"></iframe>



## 실행결과

<iframe width="560" height="315" src="https://www.youtube.com/embed/qgFVhovFero" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


참고문서

[언리얼 API](http://api.unrealengine.com/KOR/Engine/Physics/Tracing/HowTo/SingleLineTraceByObject/)