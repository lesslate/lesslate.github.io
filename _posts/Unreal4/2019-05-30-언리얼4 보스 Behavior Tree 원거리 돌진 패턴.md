---
title: "언리얼4 보스 Behavior Tree 원거리 돌진 패턴"
categories: 
  - Unreal4
last_modified_at: 2019-05-30T13:00:00+09:00
tags: 
  - unreal4 
  - Behavior Tree
  - Blueprint
  - C++
toc: true
sidebar_main: true
---

## Intro

> - 거리에 따른 패턴 추가

## 거리 측정 서비스 생성

```cpp
UBTService_Distance::UBTService_Distance()
{
	NodeName = TEXT("Distance");
	Interval = 1.0f;
}

void UBTService_Distance::TickNode(UBehaviorTreeComponent & OwnerComp, uint8 * NodeMemory, float DeltaSeconds)
{
	Super::TickNode(OwnerComp, NodeMemory, DeltaSeconds);

	APawn* ControllingPawn = OwnerComp.GetAIOwner()->GetPawn();
	if (nullptr == ControllingPawn) return;

	auto Grux = Cast<AGrux>(OwnerComp.GetAIOwner()->GetPawn());

	bool bResult;

	auto Target = Cast<ARaidPlayer>(OwnerComp.GetBlackboardComponent()->GetValueAsObject(AGruxAIController::TargetKey));
	
	if (nullptr == Target)
		return;

	bResult = (Target->GetDistanceTo(ControllingPawn) >= 1000.0f);
	
	OwnerComp.GetBlackboardComponent()->SetValueAsBool(AGruxAIController::Distance, bResult);
}

```

캐릭터와 몬스터의 거리가 1000이 넘으면 true를 반환하는 서비스

## Behavior Tree 구성

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Dashattack/1.png?raw=true)

공격 할수없는 상태일때 서비스는 거리에따라 블랙보드의 Distance bool변수를 변화시키고 false 상태일땐 추격을 true 상태일땐 돌진하여 공격애니메이션을 재생하도록 구성 

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Dashattack/2.png?raw=true)

돌진 할때 WalkSpeed를 2000으로 변경하는 서비스 추가

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Dashattack/3.png?raw=true)

이동속도가 1000이 넘을때 돌진 애니메이션을 재생하도록 AnimBlueprint 수정

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Dashattack/4.png?raw=true)

`Distance`가 1000이하일때  거리가 1000이상 벌어지면 중단하고 바로 돌진패턴을 시작하도록 `On Value Change`로 수정

## 실행 결과

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/Dashattack/GIF.gif?raw=true)

