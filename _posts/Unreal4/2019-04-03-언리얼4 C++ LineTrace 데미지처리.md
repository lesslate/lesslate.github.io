---
title: "언리얼4 C++ LineTrace 데미지처리와 충돌 이펙트"
categories: 
  - Unreal4
last_modified_at: 2019-04-03T13:00:00+09:00
tags: 
  - unreal4 
  - C++
  - Blueprint
toc: true
sidebar_main: true
---

## Intro

> - LineTrace 데미지처리

## LineTrace 사용

```cpp
FHitResult OutHit;
FVector Start = FollowCamera->GetComponentLocation(); // 시작점
FVector ForwardVector = FollowCamera->GetForwardVector();
FVector End = (Start + (ForwardVector*10000.f));  // 끝점
FCollisionQueryParams CollisionParams;
CollisionParams.AddIgnoredActor(this); // 제외할 액터

DrawDebugLine(GetWorld(), Start, End, FColor::Green, true); // 디버그라인 생성

bool isHit = GetWorld()->LineTraceSingleByChannel(OutHit, Start, End, ECC_Visibility, CollisionParams);
```

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/LinetraceDamage/1.png?raw=true)

카메라부터 카메라 전방 100미터까지 추적하여 부딪히는 액터 반환

## 데미지 처리

```cpp
if (isHit)
{
    if (OutHit.GetActor())
    {
    DrawDebugSolidBox(GetWorld(), OutHit.ImpactPoint, FVector(10.f), FColor::Blue, true); // 디버그박스
    UE_LOG(LogTemp, Log, TEXT("Hit Actor : %s"), *OutHit.GetActor()->GetName()); // 맞은 액터 이름 출력
    UE_LOG(LogTemp, Log, TEXT("Hit Bone : %s"), *OutHit.BoneName.ToString()); // 맞은 Bone이름 출력
    AActor* HitActor = OutHit.GetActor();
    GameStatic->ApplyPointDamage(HitActor, 50.0f, HitActor->GetActorLocation(), OutHit, nullptr, this,nullptr); // 데미지
    }
}
```

`HitActor`에 라인트레이스에 충돌한 액터를 저장하고 그 액터에게 `ApplyPointDamage` 함수로 `50.0f` 만큼의 데미지를 전달


![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/LinetraceDamage/3.png?raw=true)

좀비 블루프린트에서 `PointDamage` 이벤트를 받아 `HP`값을 깎고 0이하가 되면 죽는 모션을 취하게끔 함 또한 맞은 `BoneName`이 `Head`라면 
HeadShot 문구를 띄우고 바로 죽는 로직으로 가게했다. 

이때 다음과같이 `CapsulComponent`의 콜리전 트레이스 반응은 무시로 `Mesh`의 콜리전반응을 블록으로 바꿔야 정상적으로 `BoneName`이 저장될수 있다.

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/LinetraceDamage/44.png?raw=true)


## 이펙트 추가

```cpp
if (OutHit.GetActor()->ActorHasTag("Monster"))
{
    GameStatic->SpawnEmitterAtLocation(GetWorld(), BloodParticle, OutHit.ImpactPoint); 
}
else
{
    GameStatic->SpawnEmitterAtLocation(GetWorld(), SmokeParticle, (OutHit.ImpactPoint)+(OutHit.ImpactNormal*20)); 
}
```
충돌 액터의 태그가 `Monster`이라면 맞은 지점에 피 이펙트를 재생하고 그외엔 연기이펙트를 재생시키게끔 했다.
`(OutHit.ImpactPoint)+(OutHit.ImpactNormal*20)` 이부분에서 ImpactPoint는 충돌 위치를 나타내고 ImpactNormal은 충돌한 
부분의 방향벡터를 나타낸다 결국 맞은 지점에서 20만큼 떨어진곳에 연기 이펙트를 재생시켜 좀더 잘보이게끔 했다.

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/LinetraceDamage/2.png?raw=true)

몬스터와 사물의 이펙트가 다른 모습

## 실행 결과

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/LinetraceDamage/GIF.gif?raw=true)


## 참고문서
