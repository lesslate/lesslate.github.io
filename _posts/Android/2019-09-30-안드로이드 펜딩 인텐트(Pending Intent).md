---
title: "안드로이드 펜딩 인텐트(Pending Intent)"
categories: 
  - Android
last_modified_at: 2019-09-30T13:30:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> Pending Intent에 대해서 알아보기


## Pending Intent

`PendingIntent`는 `Intent`를 가지고 있는 클래스로 가지고있는 인텐트를 보류하고 특정 시점에 작업을 요청 하도록 하는 특징을 가지고 있다.

`Notification`을 통해 인텐트를 실행 하도록 하거나 특정 시점에 `AlarmManger`를 이용하여 인텐트를 실행 할 때 사용한다.

> Activity를 시작하는 인텐트

`getActivity(Context, int, Intent, int)`

> BroadcastRecevier를 시작하는 인텐트

`getBroadcast(Context, int, Intent, int)`

> Service를 시작하는 인텐트

`getService(Context, int, Intent, int)

## 예제

```java
Intent intent = new Intent(this, MainActivity.class);

        PendingIntent pendingIntent = PendingIntent.getActivity(this,
                0,
                intent,
                PendingIntent.FLAG_CANCEL_CURRENT);
```

위의 `PendingIntent`를 통해 `Notification`을 클릭하면 `MainActivity`가 실행된다.

> 각 FLAG의 의미

**FLAG_CANCEL_CURRENT** : 이전에 생성한 `PendingIntent`는 취소하고 새로 만든다.

**FLAG_IMMUTABLE** : 생성된 `PendingIntent`를 수정 불가능 하게 한다.

**FLAG_NO_CREATE** : 생성된 `PendingIntent` 를 반환한다.(재사용 가능)

**FLAG_ONE_SHOT** : 해당 Flag로 생성한 `PendingIntent`는 일회성이다.

**FLAG_UPDATE_CURRENT** : 이미 생성된 `PendingIntent`가 존재하면 해당 `Intent`의 `Extra Data`를 대체




## 실행 결과

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/pendingintent.gif?raw=true)

## 참고자료

[https://developer.android.com/reference/android/app/PendingIntent](https://developer.android.com/reference/android/app/PendingIntent)