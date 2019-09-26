---
title: "안드로이드 Shared Preference"
categories: 
  - Android
last_modified_at: 2019-09-26T13:00:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> Shared Preference 알아보기


## Share Preference

`Share Preference`는 안드로이드에서 Key/Value 형태의 자료구조로 데이터를 저장할 수있는 방식이다.

대용량데이터일 때 로딩이 느리므로 주료 간단한 설정을 저장하는데 사용한다.

## 사용법


> SharedPreference 클래스 생성

```java
public class SharedPref
{
    private SharedPreferences mySharedPref;
    private Context context;


    public SharedPref(Context context)
    {
        mySharedPref = context.getSharedPreferences("pref", Context.MODE_PRIVATE);
    }
    public void setNightModeState(boolean state)
    {
        SharedPreferences.Editor editor = mySharedPref.edit();
        editor.putBoolean("NightMode",state);
        editor.apply();
    }

    public Boolean loadNightModeState()
    {
        return mySharedPref.getBoolean("NightMode",false);
    }

}
```
생성자에서 `pref`라는 파일에 `MODE_PRIVATE`모드로 저장하도록 생성자를 만들어준다음 상태를 저장하고 불러오는 메소드를 정의했다.

MODE에는 총3가지가 있다

[MODE_PRIVATE : 이 앱안에서 데이터 공유]

[MODE_WORLD_READABLE : 다른 앱과 데이터 읽기 공유]

[MODE_WORLD_WRITEABLE : 다른 앱과 데이터 쓰기 공유]

`setNightModeState`와 `loadNightModeState` 테마 설정 상태를 저장하고 불러오도록 한다. 이때 키 값은 `NightMode`이다.

> SharedPreference 사용

```java
private SharedPref sharedPref;

sharedPref = new SharedPref(getActivity());

sharedPref.setNightModeState(값);
sharedPref.loadNightModeState()

```
객체를 생성하고 값을 저장할때는 `sharedPref.setNightModeState(값);`을

불러올때는 `sharedPref.loadNightModeState()`을 사용한다.


## 실행 결과

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/shared%20preference/GIF.gif?raw=true)


