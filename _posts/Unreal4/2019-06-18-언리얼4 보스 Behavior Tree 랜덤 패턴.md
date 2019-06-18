---
title: "언리얼4 보스 Behavior Tree 랜덤 패턴"
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

> - 몬스터 랜덤 패턴

## 난수를 이용한 랜덤 패턴


> AI 컨트롤러에 키 추가

```cpp
static const FName SelectAttackNumber; // 헤더

const FName AGruxAIController::SelectAttackNumber(TEXT("SelectAttackNumber"));
```

> 난수를 통해 정수를 저장하는 서비스



```cpp
UBTService_RandomNumber::UBTService_RandomNumber()
{
	NodeName = TEXT("CreateRandomNumber");
	Interval = 1.0f;

	bNotifyBecomeRelevant = true;
}

void UBTService_RandomNumber::OnBecomeRelevant(UBehaviorTreeComponent& OwnerComp, uint8* NodeMemory)
{
	Super::OnBecomeRelevant(OwnerComp, NodeMemory);

	int x = 0;
	x = FMath::RandRange(1, 100);

	

	if (x <=10)
	{
		OwnerComp.GetBlackboardComponent()->SetValueAsInt(AGruxAIController::SelectAttackNumber, 1);
	}
	else if (x <= 20)
	{
		OwnerComp.GetBlackboardComponent()->SetValueAsInt(AGruxAIController::SelectAttackNumber, 2);
	}
	else if (x <= 50)
	{
		OwnerComp.GetBlackboardComponent()->SetValueAsInt(AGruxAIController::SelectAttackNumber, 3);
	}
	else if (x <= 80)
	{
		OwnerComp.GetBlackboardComponent()->SetValueAsInt(AGruxAIController::SelectAttackNumber, 4);
	}
	else
	{
		OwnerComp.GetBlackboardComponent()->SetValueAsInt(AGruxAIController::SelectAttackNumber, 5);
	}

}
```

1부터 100사이의 난수를 발생시켜 블랙보드 `SelectAttackNumber` 키에 10이하는 1, 10~20은 2, 20~50은 3, 50~80은 4, 나머지는 5를 저장한다.

> 데코레이터 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/SelectRandom/1.png?raw=true)

블랙보드 데코레이터를 추가한다음 자주 사용하게할 패턴은 자주나오는 3번과 4번값과 같을때 Select되도록 한다.


![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/SelectRandom/2.png?raw=true) 

마찬가지로 원거리 패턴에도 똑같이 적용시켜준다.
![GIF](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/BackJump/GIF.gif?raw=true)

> 서비스 추가

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unreal/SelectRandom/3.png?raw=true)

난수를 발생시키는 서비스는 트리 위쪽에 배치한다.

## 참고 자료
