---
title: "언리얼4 보스 Behavior Tree 범위 패턴"
categories: 
  - Unreal4
last_modified_at: 2019-06-18T13:00:00+09:00
tags: 
  - unreal4 
  - Behavior Tree
  - C++

toc: true
sidebar_main: true
---

## Intro

> - 몬스터 범위 패턴 추가

## 패턴 개요

일정 범위안에 데미지를 주도록 하는 패턴 구현

## 비헤이비어 트리 추가

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Quake/2.png?raw=true)

## 애니메이션 노티파이 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Quake/1.png?raw=true)

`RadialDamage` 노티파이 호출

> AnimInstance

```cpp
void UGruxAnimInstance::AnimNotify_RadialDamage()
{
	Grux->RadialDamage();
}
```

> 몬스터 액터

```cpp
void AGrux::RadialDamage()
{
	ServerApplyRadialDamage(Damage*2.0, 1000);
}
```

데미지와 범위 파라메터를 전달 해준다.


```cpp
void AGrux::ServerApplyRadialDamage_Implementation(float RDamage,float Radius)
{
	UGameplayStatics::ApplyRadialDamage(GetWorld(), RDamage, this->GetActorLocation(), Radius, nullptr, TArray<AActor*>(), this, false, ECC_GameTraceChannel5);
	GruxLeftCheck->SetCollisionEnabled(ECollisionEnabled::NoCollision);
	GruxRightCheck->SetCollisionEnabled(ECollisionEnabled::NoCollision);

	FVector Center = this->GetActorLocation();
	UWorld* World = GetWorld();

	TArray<FOverlapResult> OverlapResults;
	FCollisionQueryParams CollisionQueryParam(NAME_None, false, this);
	bool bResult = World->OverlapMultiByChannel(
		OverlapResults,
		Center,
		FQuat::Identity,
		ECollisionChannel::ECC_GameTraceChannel5,
		FCollisionShape::MakeSphere(Radius),
		CollisionQueryParam
	);
	if (bResult)
	{
		for (auto OverlapResult : OverlapResults)
		{
			ARaidPlayer* Player = Cast<ARaidPlayer>(OverlapResult.GetActor());
			if (Player != nullptr)
			{
				CHECK(Player != nullptr);
				FVector PlayerLocation = Player->GetActorLocation();
				FTransform PlayerTransform = Player->GetActorTransform();
				if (!Player->IsDodge)
				{
					UGameplayStatics::PlaySoundAtLocation(this, GruxGroundHit, PlayerLocation);
					UGameplayStatics::SpawnEmitterAtLocation(GetWorld(), GruxFireEffect, PlayerTransform, true);
				}
			}
		}
	}
}
```

데미지 전달과 함께 범위내에 플레이어가 있으면 피격사운드와 파티클을 재생시키도록 했다.

if문을 통해 플레이어의 상태가 구르기 상태(무적)가 아닐때만 발생시키도록함

## 실행 결과

![GIF](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Quake/GIF.gif?raw=true)

## 참고 자료
