---
title: "안드로이드 현재 날짜, 시간 출력"
categories: 
  - Android
last_modified_at: 2019-09-07T13:00:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> 현재 날짜, 시간 가져오기

## 현재 날짜 시간 구하기

> 현재 시간 구하기

```java
long now = System.currentTimeMillis();
```

> 현재 시간을 날짜에 저장

```java
Date date = new Date(now);
```

> 날짜,시간을 나타내려고 하는 포맷 지정

```java
SimpleDateFormat mFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
```

> String 변수 저장

```java
String time = mFormat.format(date);
```

## 예제

```java

import java.util.Date;
import java.text.SimpleDateFormat;


private TextView whenDate;
private SimpleDateFormat mFormat = new SimpleDateFormat("yyyy/M/d"); // 날짜 포맷


    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState)
    {
        view = inflater.inflate(R.layout.frag2, container, false);

        whenDate = (TextView) view.findViewById(R.id.whenDate);
      
        Date date = new Date();
        String time = mFormat.format(date);
        whenDate.setText(time); // 현재 날짜로 설정
    }
```


## 실행 결과

![date](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/date.png?raw=true)