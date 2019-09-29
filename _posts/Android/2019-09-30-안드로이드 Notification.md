---
title: "안드로이드 Notification"
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

> Notification 사용하기


## Notification 구현

```java
public void show()
{
    // 알람 표시할지 스위치 상태
    if(!sharedPref.loadAlarm())
    {
        return; // false일시 알람을 띄우지않음
    }
 
    // 내용 초기화
    mDialogContent.setLength(0);
 
    dbHelper = MemoDBHelper.getInstance(this);
    String[] params = {mTime};
    Cursor cursor = (Cursor) dbHelper.getReadableDatabase().query(MemoContract.MemoEntry.TABLE_NAME, null, "date=?", params, null, null, null);
    
    cursor.moveToFirst();

    if (cursor != null && cursor.getCount() != 0)
    {
        if (cursor.getCount() == 1) // 일정이 1개 일시
        {
            mDialogContent.append(cursor.getString(cursor.getColumnIndexOrThrow(MemoContract.MemoEntry.COLUMN_NAME_TITLE))); // 커서 첫줄을 표시
        } 
        else
        {
            mDialogContent.append(cursor.getString(cursor.getColumnIndexOrThrow(MemoContract.MemoEntry.COLUMN_NAME_TITLE))); // 커서 첫줄 제목과 그외 갯수 표시
            mDialogContent.append(" 외 ");
            mDialogContent.append(cursor.getCount() - 1);
            mDialogContent.append("개의 일정이 있습니다.");
        }
    } 
    else
    {
        mDialogContent.append("오늘의 일정이 없습니다."); // 일정이 없을 경우
    }


    NotificationCompat.Builder builder = new NotificationCompat.Builder(this, "default");
    builder.setSmallIcon(R.mipmap.ic_launcher_calendar); // 아이콘
    builder.setContentTitle("오늘의 일정"); // 제목
    builder.setContentText(mDialogContent.toString()); // 내용
    
    Intent intent = new Intent(this, MainActivity.class);

    PendingIntent pendingIntent = PendingIntent.getActivity(this,
            0,
            intent,
            PendingIntent.FLAG_CANCEL_CURRENT);
    
    builder.setContentIntent(pendingIntent);
    Bitmap largeIcon = BitmapFactory.decodeResource(getResources(),
            R.mipmap.ic_launcher_calendar);
    builder.setLargeIcon(largeIcon);
    builder.setAutoCancel(false);

    NotificationManager manager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O)
    {
        manager.createNotificationChannel(new NotificationChannel("default", "기본 채널", NotificationManager.IMPORTANCE_LOW));
        manager.getNotificationChannel("default").setVibrationPattern(new long[]{ 0 }); // 진동제거
        manager.getNotificationChannel("default").enableVibration(true);

    }


    manager.notify(1, builder.build());
    }
```

데이터 베이스에 저장된 일정을 `StringBuffer`인 `mDialogContent`에 저장시킨 다음 `NotificationCompat.Builder` 개체를 생성하고 제목, 아이콘 , 내용(mDialogContent)를 세팅했다.

그리고 `PendingIntent`에 액티비티에 대한 정보를 담은다음 `NotificationChannel` 를 구성 해주었다.

`NotificationChannel` 은 안드로이드8.0(오레오) 부터 필수로 사용되었으며 채널을 통해 각각의 `Notification`의 진동이나 소리등의 중요도를 관리 할 수 있다.

마지막으로 알림은 `manager.notify(1, builder.build());` 메서드로 실행할 수 있다.


또한 `manager.cancel(1);`은 해당 ID를 가진 알림을 삭제한다.



## 실행 결과

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/notification/1.png?raw=true)

## 참고자료

[https://developer.android.com/guide/topics/ui/notifiers/notifications?hl=ko](https://developer.android.com/guide/topics/ui/notifiers/notifications?hl=ko)