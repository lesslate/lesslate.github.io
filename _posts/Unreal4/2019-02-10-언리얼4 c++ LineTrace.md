---
title: "언리얼4 C++ LineTrace"
categories: 
  - Unreal4
last_modified_at: 2019-02-10T13:00:00+09:00
tags: 
  - unreal4 
  - LineTrace
  - C++
toc: true
sidebar_main: true
---

## Intro

> - C++ Line Trace


## 플레이어 뷰포인트 가져오기

<script src="https://gist.github.com/lesslate/0cdf01eb984ca3eaa4274ed872228a92.js"></script>


## 디버그 라인 그리기

헤더파일에 Reach변수 선언

```cpp
private:
	float Reach = 100.f;
```

플레이어가 바라보는 방향과 `Reach`를 이용하여 LineTraceEnd 저장

```cpp

FVector LineTraceEnd = PlayerViewPointLocation + PlayerViewPointRotation.Vector()*Reach;

```

DrawDebugLine 함수로 디버그 라인 생성 

<script src="https://gist.github.com/lesslate/5837e1ae5b667efed571282ea4804333.js"></script>

> 생성된 디버그 라인

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Linetrace/1.png?raw=true)

## 라인 트레이스로 충돌 체크

<script src="https://gist.github.com/lesslate/ce9a9b717da5d2651458f9122c8a335e.js"></script>


성공적으로 출력되는 로그

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Linetrace/2.png?raw=true)



## 참고문서

[https://unrealcpp.com/line-trace-on-tick/](https://unrealcpp.com/line-trace-on-tick/)

[http://api.unrealengine.com/INT/API/Runtime/Engine/Engine/UWorld/LineTraceSingleByObjectType/](http://api.unrealengine.com/INT/API/Runtime/Engine/Engine/UWorld/LineTraceSingleByObjectType/)

[http://api.unrealengine.com/INT/API/Runtime/Engine/FCollisionQueryParams/](http://api.unrealengine.com/INT/API/Runtime/Engine/FCollisionQueryParams/)
