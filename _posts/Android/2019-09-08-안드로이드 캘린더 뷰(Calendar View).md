---
title: "안드로이드 캘린더 뷰(Calendar View)"
categories: 
  - Android
last_modified_at: 2019-09-08T13:00:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> Calendar View 알아보기


## 캘린더 뷰 XML 속성

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/calendar/1.png?raw=true)

`firstDayOfWeek` : 제일 왼쪽의 첫 요일 (1: 일요일 , 2: 월요일)

`minDate` : 달력에 표시할 최소 날짜

`maxDate` : 달력에 표시할 최대 날짜

`focusedMonthDateColor` : 현재 선택된 달의 배경 색

`selectedWeekBackgroundColor` : 선택된 주의 배경 색

`unfocusedMonthDateColor` : 선택되지 않은 달의 배경 색상

`showWeekNumber` : 왼쪽에 주차를 표시할 지 여부

`weekNumberColor` : 주의 색 지정

`weekSeparatorLineColor` : 주 사이의 구분선

## 캘린더 뷰 메서드

```java
long getDate()
```

날짜 조사 메서드


```java
void setDate(long date [, boolean animate, boolean center])
```


날짜 변경 메서드

```java
void setOnDateChangeListener(CalendarView.OnDateChangeListener listener)
```

날짜가 변경될 때 이벤트를 받기 위한 리스너

```java
void onSelectedDayChange(CalendarView view, int year, int month, int dayOfMonth)
```

선택된 날짜를 알려주는 메서드


## 예제

> 선택된 날짜를 텍스트로 변환하는 과정 

```java
public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState)
    {
        view = inflater.inflate(R.layout.frag2, container, false);

        mCalendarView = (CalendarView) view.findViewById(R.id.calendarView);
        whenDate = (TextView) view.findViewById(R.id.whenDate);

   mCalendarView.setOnDateChangeListener(new CalendarView.OnDateChangeListener() // 날짜 선택 이벤트
        {
            @Override
            public void onSelectedDayChange(@NonNull CalendarView view, int year, int month, int dayOfMonth)
            {
                String date = year + "/" + (month + 1) + "/" + dayOfMonth;
                whenDate.setText(date); // 선택한 날짜로 설정

            }
        });
    }
```

## 실행 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/calendar/2.png?raw=true)