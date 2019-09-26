---
title: "안드로이드 액션바 (ActionBar)"
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

> 액션바 활용하기


## 액션바 (ActionBar)

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/ActionBar/1.png?raw=true)

액션바는 여러 종류의 위젯으로 구성된 도구모음이다.


## 액션바 사용

> styles.xml

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
```

기본 테마에는 `ActionBar`를 사용를 사용하게 되어있다.

액션바를 사용하지 않으려면 `Theme.AppCompat.Light.NoActionBar`을 상속받는다.

> Action 추가하기

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">


<item
    android:id="@+id/action_search"
    android:icon="@drawable/ic_check_black_24dp"
    android:title="Search"
    app:showAsAction="always" />
    
</menu>
```

액션으로 사용할 `item` xml파일 추가한다.

이때 `showAsAction` 속성은 5가지로 지정할 수 있다.

`always` - 항상 액션으로 표시

`never` - 액션으로 표시하지않고 오버플로우 메뉴에 표시

`ifRoom` - 공간이있다면 액션으로 표시, 없다면 오버플로우 메뉴에 표시

`withText` - 액션과 텍스트를 같이 표시

`collapseActionView` 커스텀 액션 뷰가 지정된 경우 축소된 형태로 표시


```java
 @Override
public boolean onCreateOptionsMenu(Menu menu)
{
    getMenuInflater().inflate(R.menu.actionbar_actions, menu) ;
    return super.onCreateOptionsMenu(menu);
}
```    

만들어둔 액션을 액티비티에서 `inflate` 해주면 상단 액션바에 표시가 된다.

## 액션 이벤트

```java
@Override
public boolean onOptionsItemSelected(MenuItem item)
{
    int id = item.getItemId();
    if(id==R.id.action_search)
    {
        onBackPressed();
    }
    return super.onOptionsItemSelected(item);
}
```    

`onOptionsItemSelected` 메소드에서 클릭한 액션의 id를 통해 각각의 이벤트를 구성해준다.


## 액션바 설정

```java
ActionBar actionBar = ((MainActivity)getActivity()).getSupportActionBar();

actionBar.setTitle("오늘의 일정");
```

```java
androidx.appcompat.app.ActionBar actionBar = ((MainActivity) getActivity()).getSupportActionBar();

actionBar.setTitle("설정");
```

위와 같이 `Activity`나 `Fragment` 에서 액션바의 설정을 따로 변경할 수 있다.

## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/ActionBar/1.gif?raw=true)

## 참고자료

[https://recipes4dev.tistory.com/141](https://recipes4dev.tistory.com/141)

