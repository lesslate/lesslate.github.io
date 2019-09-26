---
title: "안드로이드 Preference"
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

> Preference 사용하기


## Preference

`PreferenceFragment` 혹은 `PreferenceActivity` 컴포넌트를 사용하면 쉽게 설정창을 구성할 수 있다.


## 사용방법

> Gradel 추가

```java
implementation 'com.android.support:preference-v7:28.0.0'
```

> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <PreferenceCategory
        android:title="데이터 설정" />

    <Preference
        android:key="reset"
        android:title="일정 초기화">
    </Preference>


    <PreferenceCategory
        android:title="테마 설정"
        />

    <SwitchPreferenceCompat
        android:key="theme_setting"
        android:title="블랙 테마"
        android:enabled="true" >
    </SwitchPreferenceCompat>

    <PreferenceCategory
        android:title="기타"
        />

    <Preference
        android:key="review"
        android:title="구글스토어 리뷰">
    </Preference>

    <Preference
        android:key="feedback"
        android:title="피드백/건의">
    </Preference>


</PreferenceScreen>
```

PreferenceXML을 구성해준다.

다음과 같은 구성요소들이 있다.

`PreferenceCategory`

`CheckBoxPreference`

`Preference`

`SwitchPreferenceCompat`

`EditTextPreference`

`ListPreference`

> Fragement.java

```java
public class Frag3 extends PreferenceFragmentCompat
```

`PreferenceFragmentCompat`를 상속받고 `onCreatePreferences`에서 준비한 xml을 가져오도록 한다.

```java
@Override
public void onCreatePreferences(Bundle savedInstanceState, String rootKey)
{
    addPreferencesFromResource(R.xml.settings_preference);
}
```


## Preference 클릭 이벤트

```java
private Preference resetPreference;
private Preference sendFeedback;

public void onCreatePreferences(Bundle savedInstanceState, String rootKey)
{

dbHelper = MemoDBHelper.getInstance(getActivity());
resetPreference = (Preference) findPreference("reset");
sendFeedback = (Preference) findPreference("feedback");

// 일정 초기화
resetPreference.setOnPreferenceClickListener(new Preference.OnPreferenceClickListener()
{
    @Override
    public boolean onPreferenceClick(Preference preference)
    {
        builder.setTitle("초기화");
        builder.setMessage("모든 일정을 삭제하시겠습니까?");
        builder.setPositiveButton("삭제", new DialogInterface.OnClickListener()
        {
            @Override
            public void onClick(DialogInterface dialog, int which)
            {
                SQLiteDatabase db = dbHelper.getWritableDatabase();
                dbHelper.DropTable(db);
                Toast.makeText(getActivity(), "모든 일정이 삭제되었습니다", Toast.LENGTH_SHORT).show();
            }
        });
        builder.setNegativeButton("취소", null);
        builder.show();
        return false;
    }
});

// 피드백 메일보내기
sendFeedback.setOnPreferenceClickListener(new Preference.OnPreferenceClickListener()
{
    @Override
    public boolean onPreferenceClick(Preference preference)
    {
        Intent email = new Intent(Intent.ACTION_SEND);
        email.setType("plain/text");
        String[] address = {"lesslate9@naver.com"};
        email.putExtra(Intent.EXTRA_EMAIL, address);
        email.putExtra(Intent.EXTRA_SUBJECT, "");
        email.putExtra(Intent.EXTRA_TEXT, "");
        startActivity(email);
        
        return false;
    }
});
}

```

일정 초기화와 메일 보내기를 구현하였다. 

일정초기화 Preference를 누르면 Dialog를 띄우고 확인시 DBHelper의 메소드를 통해 테이블의 모든 레코드를 삭제한다.

```java
public void DropTable(SQLiteDatabase db)
{
    db.delete(MemoContract.MemoEntry.TABLE_NAME, null, null);
}
```

메일보내기는 암시적 인텐트를 통해 이메일 앱이 실행되도록 했다.

## 실행 결과

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/preferenceFragment/33.gif?raw=true)

## 참고자료

[https://developer.android.com/reference/android/support/v7/preference/PreferenceFragmentCompat](https://developer.android.com/reference/android/support/v7/preference/PreferenceFragmentCompat)

