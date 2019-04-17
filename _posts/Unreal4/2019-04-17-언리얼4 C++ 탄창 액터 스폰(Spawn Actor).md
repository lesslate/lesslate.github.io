---
title: "언리얼4 C++ 탄창 액터 스폰 (Spawn Actor)"
categories: 
  - Unreal4
last_modified_at: 2019-04-17T13:00:00+09:00
tags: 
  - unreal4 
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 랜덤 탄창 드랍 구현

## 스폰할 액터 저장

> 탄창 액터 선언
```cpp
UPROPERTY(EditAnywhere)
TSubclassOf<class AActor> AmmoBlueprint;
```

> 인스턴스 저장
```cpp
static ConstructorHelpers::FObjectFinder<UBlueprint> AmmoItem(TEXT("Blueprint'/Game/Weapon/Ammo.Ammo'"));
if (AmmoItem.Object)
{
	AmmoBlueprint = (UClass*)AmmoItem.Object->GeneratedClass;
}
```


## 액터 스폰

```cpp
int32 Random=FMath::RandRange(1, 10);
	
	if (Random == 1&&AmmoBlueprint)
	{
		UWorld* world = GetWorld();
		if (world)
		{
			UE_LOG(LogTemp, Log, TEXT("SpawnAmmo"));
			FActorSpawnParameters SpawnParams;
			SpawnParams.Owner = this;
			FRotator rotator;
			FVector  SpawnLocation = GetActorLocation();
			SpawnLocation.Z -= 90.0f;
			
			world->SpawnActor<AActor>(AmmoBlueprint, SpawnLocation, rotator, SpawnParams);
		}
	}
}
```

몬스터가 죽을때 실행되는 `Death`함수에 탄창 액터를 스폰시키도록 한다.

이때 1부터 10까지 난수를 발생시키고 1일때 스폰시키도록 하여 10%의 확률을 주었다.


## 실행 결과

죽은 자리에 스폰되는 탄창 액터

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/SpawnItem/1.png?raw=true)



## 참고문서

[http://api.unrealengine.com/KOR/Programming/UnrealArchitecture/Actors/Spawning/](http://api.unrealengine.com/KOR/Programming/UnrealArchitecture/Actors/Spawning/)