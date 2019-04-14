---
title: "언리얼4 C++ 데미지 적용"
categories: 
  - Unreal4
last_modified_at: 2019-04-10T13:00:00+09:00
tags: 
  - unreal4 
  - C++
  - BehaviorTree
toc: true
sidebar_main: true
---

## Intro

> - C++ 데미지 적용하기

## 플레이어가 주는 데미지

> ApplyPointDamage

```cpp
if (OutHit.GetActor()->ActorHasTag("Monster")) 
{
    GameStatic->ApplyPointDamage(HitActor, 50.0f, HitActor->GetActorLocation(), OutHit, nullptr, this, nullptr); // 포인트 데미지
}
```

플레이어는 라인트레이스를 이용해 태그가 Monster인 액터와 충돌시 `PointDamage` 함수를 호출해서 데미지를 전달한다.


> ReceivePointDamage

몬스터는 다음과같이 `ReceivePointDamage` 함수를 호출하게되고 히트된 `BoneName`이 `Head`라면 바로 `Death`함수를 호출하고 아니라면 
`HP`변수에서 전달받은 `Damage`만큼 감소시키고 0이하가 되면 마찬가지로 `Death` 함수를 호출하도록함


```cpp
void AZombie::ReceivePointDamage(float Damage, const UDamageType * DamageType, FVector HitLocation, FVector HitNormal, UPrimitiveComponent * HitComponent, FName BoneName, FVector ShotFromDirection, AController * InstigatedBy, AActor * DamageCauser, const FHitResult & HitInfo)
{
	if (BoneName == TEXT("Head"))
	{
		IsDeath = true;
		Death();
	}
	else
	{
		HP -= Damage;
		if (HP <= 0)
		{
			Death();
		}
	}
}
```

> Death

```cpp
void AZombie::Death()
{
	ZombieAI->StopAI();
	GetCharacterMovement()->SetMovementMode(MOVE_None);
	GetCapsuleComponent()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
	GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
	ZombieAnim->PlayDeathMontage();
	AudioComponent->Stop();

}
```

`Death`함수가 호출되면 `AIController`에서 `StopAI`함수를 호출하고
이동을 비활성화 시키고 메쉬와 캡슐의 콜리전을 끄고 쓰러지는 몽타주를 재생하고 소리 큐를 정지한다.

> StopAI

```cpp
auto BehaviorTreeComponent = Cast<UBehaviorTreeComponent>(BrainComponent);
if (nullptr != BehaviorTreeComponent)
{
    BehaviorTreeComponent->StopTree(EBTStopMode::Safe);
}
```

`StopAI`에서 비헤이비어 트리를 정지시킨다

## 몬스터가 주는 데미지

> 멀티캐스트 델리게이트 선언

```cpp
DECLARE_MULTICAST_DELEGATE(FOnAttackHitCheckDelegate);

FOnAttackHitCheckDelegate OnAttackHitCheck;
```

> 노티파이로 델리게이트 사용

```cpp
void UZombieAnimInstance::AnimNotify_AttackHitCheck()
{
	OnAttackHitCheck.Broadcast();
}
```
공격 몽타주에 `AttackHitCheck` 노티파이를 추가하고 `OnAttackHitCheck` 델리게이트를 `Broadcast`해준다.

> 공격 판정 체크

```
ZombieAnim->OnAttackHitCheck.AddUObject(this, &AZombie::AttackCheck);
```
`Broadcast` 호출시 `AttackCheck` 함수가 호출된다.

> AttackCheck

```cpp
void AZombie::AttackCheck()
{
	//TArray<FHitResult> HitResult;
	FHitResult HitResult;

	FCollisionQueryParams Params;
	Params.AddIgnoredActor(this);
	bool bResult = GetWorld()->SweepSingleByChannel(
		HitResult,
		GetActorLocation(),
		GetActorLocation() + GetActorForwardVector() * 50.0f,
		FQuat::Identity,
		ECollisionChannel::ECC_GameTraceChannel5, 
		FCollisionShape::MakeSphere(50.0f),
		Params);
        
    if (bResult)
	{
		//UE_LOG(LogTemp, Log, TEXT("Zombie Hit: %s"), *HitResult.GetActor()->GetName());
			if (HitResult.GetActor()->ActorHasTag("Player"))
			{	
				FDamageEvent DamageEvent;
				
				HitResult.Actor->TakeDamage(20, DamageEvent, GetController(), this);

			}
	}
}
```

`SweepSingleByChannel` 함수를 통해 전방에 충돌체크를 하고 `Player`태그 액터가 있으면 데미지를 준다.

이때 `GameTraceChennel5`를 사용하여 같은 몬스터를 콜리전에서 제외시킨다. 

> TakeDamage

데미지를 받으면 플레이어의 `TakeDamage`함수를 통해 데미지를 전달받고 HP가 0이하가되면 `Death`를 호출한다.

```cpp
float AFPSPlayer::TakeDamage(float Damage, FDamageEvent const & DamageEvent, AController * EventInstigator, AActor * DamageCauser)
{
	const float ActualDamage = Super::TakeDamage(Damage, DamageEvent, EventInstigator, DamageCauser);
	if (ActualDamage > 0.f)
	{
		PlayerHP -= ActualDamage;
		if (PlayerHP <= 0.f)
		{
			Death();
		}
	}
	return ActualDamage;
}
```

> Death

```cpp
void AFPSPlayer::Death()
{
	FPSAnim->IsDeath = true;
	GetCharacterMovement()->SetMovementMode(MOVE_None);
	GetCapsuleComponent()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
	GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
}
```
`Death` 함수가 호출되면 쓰러지는 몽타주를 재생하고 콜리전을 비활성화한뒤 더이상 제어할수 없게한다.

## 실행 결과

![gif](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/CPPDamage/1.gif?raw=true)

![gif2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/CPPDamage/2.gif?raw=true)

## 참고문서

[https://unrealcpp.com/health-bar-ui-hud/](https://unrealcpp.com/health-bar-ui-hud/)

[http://api.unrealengine.com/INT/API/Runtime/Engine/Engine/UWorld/SweepSingleByChannel/index.html](http://api.unrealengine.com/INT/API/Runtime/Engine/Engine/UWorld/SweepSingleByChannel/index.html)

[https://api.unrealengine.com/INT/API/Runtime/Engine/GameFramework/AActor/TakeDamage/index.html](https://api.unrealengine.com/INT/API/Runtime/Engine/GameFramework/AActor/TakeDamage/index.html)