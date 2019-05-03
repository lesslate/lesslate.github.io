---
title: "언리얼4 C++ 델리게이트를 이용한 상호작용(Interaction using delegate)"
categories: 
  - Unreal4
last_modified_at: 2019-05-03T13:00:00+09:00
tags: 
  - unreal4 
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 델리게이트를 이용한 상호작용 구현

## 델리게이트(Delegate)

`Delegate`의 사전적 의미는 대리자, 대표자이며 C++에서는 지원하지않고 C#에서 지원하는 개념이다.

C++에서의 함수 포인터는 복잡하고 안정성이 떨어지는 방식이었다면 델리게이트는 간편한 문법과 안정성을가진다.
델리게이트의 특징은 이러한 간편함과 안정성 외에도 여러개의 함수를 대표해서 관리할 수 있다는 것이다.


> 델리게이트는 C++에서는 지원하지않지만 언리얼 C++은 자체 프레임웍을 통해 지원하고있다.


## 상호작용 추가

> 상호작용할 액터 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/1.png?raw=true)

상호작용할 액터를 추가하고 오버랩이벤트를 발생시키도록 한다.

2[2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/2.png?raw=true) 

오버랩 이벤트가 발생하면 UI 텍스트를 띄우고 오버랩 변수를 `true`로 변경


## 상호작용 키 함수 추가


```cpp
UFUNCTION(BlueprintNativeEvent)
void Interaction();
```

상호작용 키 F를 눌렀을때 호출될 `Interaction` 함수를 추가한다. 이때 `UFUNCTION(BlueprintNativeEvent)` 를 사용하면 
블루프린트에서 오버라이드된 함수를 사용할수있으므로 기존에 있던 상호작용(무기줍기) 함수는 블루프린트에서 구현한것을 사용하고 새로운 상호작용(폭격)은 C++에서 작성하기로 했다.

`BlueprintNativeEvent`를 사용할땐 함수 정의 뒤에 `_Implementation`를 붙여주어야한다. 

```cpp
void AFPSPlayer::Interaction_Implementation()
```

> 블루프린트 수정

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/3.png?raw=true)

기존 `Interaction` 블루프린트를 새로운 `Interaction` 함수로 교체한다음 C++에서의 부모 함수도 호출되도록 구성하였다.

> 전적으로 블루프린트에서 작성될 함수를 선언할때는 BlueprintImplementableEvent 를 사용한다.


## 델리게이트 사용

`GameMode`에 여러개의 함수를 바인딩할수 있는 `멀티캐스트 델리게이트` 선언

```cpp
DECLARE_MULTICAST_DELEGATE(FStartBomb);

public:
	AFPSGameMode();
	
	FStartBomb StartBombing;
```

> 실행할 함수들 바인딩

```cpp
UFUNCTION(BlueprintImplementableEvent, Category = "Fly")
void StartFly();


void AJet::BeginPlay()
{
	Super::BeginPlay();

	AFPSGameMode* gameMode = Cast<AFPSGameMode>(UGameplayStatics::GetGameMode(GetWorld()));
	if (gameMode != nullptr)
	{
		gameMode->StartBombing.AddUObject(this, &AJet::StartFly);
	}

}
```

전투기는 `StartFly` 함수를 바인드해준다. 블루프린트에서 구현하기위해 `BlueprintImplementableEvnet`를 붙여준다.


```cpp
UFUNCTION(BlueprintImplementableEvent, Category = "Bomb")
void Bomb();

void ABomb::BeginPlay()
{
	Super::BeginPlay();

	AFPSGameMode* gameMode = Cast<AFPSGameMode>(UGameplayStatics::GetGameMode(GetWorld()));
	if (gameMode != nullptr)
	{
		gameMode->StartBombing.AddUObject(this, &ABomb::Bomb);
	}
}
```

마찬가지로 터지게 폭탄은 `Bomb`이라는 함수를 바인드 해준다.

> 바인드된 함수들 호출

```cpp
void AFPSPlayer::Interaction_Implementation()
{
	if (OverlapRadio)
	{
		AFPSGameMode* gameMode = Cast<AFPSGameMode>(UGameplayStatics::GetGameMode(GetWorld()));
		if (gameMode != nullptr)
		{
			gameMode->StartBombing.Broadcast();
			UE_LOG(LogTemp, Log, TEXT("StartBomb"));
		}
	}
}
```

아까 구현했던 `Interaction` 함수에서 라디오와 오버랩된 상태라면 게임모드에서 델리게이트를 `BroadCast` 해주어 모든함수를 실행한다.(전투기 출발, 폭발) 

> 블루프린트 함수 구현

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/4.png?raw=true)

전투기는 `StartFly` 호출시 전투기 소리를 재생시키고 앞으로 비행하도록 구현

![6](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/6.png?raw=true)

`MovementMode`를 `Flying`으로 바꾸어주고 속도를 높여줌


![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Delegate/5.png?raw=true)

폭탄 액터는 수초뒤에 폭발 이펙트와 폭발 사운드를 재생시키고 주변에 `RadialDamage`를 주도록함

## 실행 결과

<iframe width="560" height="315" src="https://youtu.be/Jihbwjq_jgY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 참고문서

[https://m.blog.naver.com/PostView.nhn?blogId=destiny9720&logNo=220945441201&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=destiny9720&logNo=220945441201&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)

[https://m.blog.naver.com/PostView.nhn?blogId=khagaa&logNo=220852435209&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=khagaa&logNo=220852435209&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)

