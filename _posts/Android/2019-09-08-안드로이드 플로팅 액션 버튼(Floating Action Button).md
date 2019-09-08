---
title: "안드로이드 플로팅 액션 버튼(Floating Action Button)"
categories: 
  - Android
last_modified_at: 2019-09-08T13:00:00+09:00
tags: 
  - Android


toc: true
sidebar_main: true
---

## Intro

> Floating Action Button 사용하기


## 플로팅 액션 버튼 추가

플로팅 액션버튼은 화면에 떠있는 버튼으로 사용자가 편리하게 액션을 취할 수 있도록 도와준다.

> Gradle dependencies 추가

```java
implementation 'com.android.support:design:28.0.0'
```

> 플로팅 액션 버튼 생성

```xml
<com.google.android.material.floatingactionbutton.FloatingActionButton
    android:id="@+id/fab"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="end|bottom"
    android:layout_margin="16dp"
    android:clickable="true"
    app:srcCompat="@drawable/ic_add_black_24dp"/>
```

`layout_gravity`를 `end|bottom`으로 하여 오른쪽아래에 떠있도록 했다.



## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/FAB.png?raw=true)