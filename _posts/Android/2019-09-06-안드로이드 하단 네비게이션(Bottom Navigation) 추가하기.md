---
title: "안드로이드 하단 네비게이션(Bottom Navigation) 추가하기"
categories: 
  - Android
last_modified_at: 2019-09-06T13:00:00+09:00
tags: 
  - Android
  - Java


toc: true
sidebar_main: true
---

## Intro

> 하단 네비게이션 만들기

## 라이브러리 추가

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/1.png?raw=true)

`build.gradle(Module: app)` 에 `design support library`추가

## bottom_navigation_xml 작성

> menu 폴더 추가

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/2.png?raw=true)

`res` 폴더에 `menu` 폴더 추가후 xml 파일 생성

> 아이템 추가

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/action_today"
        android:enabled="true"
        android:icon="@drawable/ic_check_black_24dp"
        android:title="오늘의 일정"/>

    <item
        android:id="@+id/action_add"
        android:enabled="true"
        android:icon="@drawable/ic_event_available_black_24dp"
        android:title="일정 추가"/>

    <item
        android:id="@+id/action_setting"
        android:enabled="true"
        android:icon="@drawable/ic_settings_black_24dp"
        android:title="설정"/>

</menu>
```

![3](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/3.png?raw=true)

사용되는 아이콘은 `drawable`폴더에 안드로이드에서 제공하는 `Vector asset`를 사용했다.


## Activity에 Navigation 추가

![4](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/4.png?raw=true)

```xml
 <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomNavi"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:itemBackground="@android:color/white"
        app:itemIconTint="#000000"
        app:itemTextColor="#000000"
        app:layout_constraintBottom_toBottomOf="parent"
        app:menu="@menu/bottom_navigation"
        tools:layout_editor_absoluteX="16dp" />

    <FrameLayout
        android:id="@+id/Main_Frame"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintBottom_toTopOf="@+id/bottomNavi"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

    </FrameLayout>
```

메인 Activity에 프레임 레이아웃과 네비게이션뷰를 추가했다.

## Fragment 추가

![5](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/5.png?raw=true)

프레임 레이아웃에서 교체될 `Fragment` `XML`을 만들고 `inflater`로 `view`를 생성해준다.

```java
public class Frag1 extends Fragment // Fragment 클래스를 상속받아야한다
{

    private View view;


    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState)
    {
       view = inflater.inflate(R.layout.frag1,container,false);

       return view;
    }
}
```

## Navigation 이벤트


```java
public class MainActivity extends AppCompatActivity
{
    private BottomNavigationView bottomNavigationView; // 바텀 네비게이션 뷰
    private FragmentManager fm;
    private FragmentTransaction ft;
    private Frag1 frag1;
    private Frag2 frag2;
    private Frag3 frag3;

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottomNavigationView = findViewById(R.id.bottomNavi);
        bottomNavigationView.setOnNavigationItemSelectedListener(new BottomNavigationView.OnNavigationItemSelectedListener()
        {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem menuItem)
            {
                switch (menuItem.getItemId())
                {
                    case R.id.action_today:
                        setFrag(0);
                        break;
                    case R.id.action_add:
                        setFrag(1);
                        break;
                    case R.id.action_setting:
                        setFrag(2);
                        break;
                }
                return true;
            }
        });

        frag1=new Frag1();
        frag2=new Frag2();
        frag3=new Frag3();
        setFrag(0); // 첫 프래그먼트 화면 지정
    }

    // 프레그먼트 교체
    private void setFrag(int n)
    {
        fm = getSupportFragmentManager();
        ft= fm.beginTransaction();
        switch (n)
        {
            case 0:
                ft.replace(R.id.Main_Frame,frag1);
                ft.commit();
                break;

            case 1:
                ft.replace(R.id.Main_Frame,frag2);
                ft.commit();
                break;

            case 2:
                ft.replace(R.id.Main_Frame,frag3);
                ft.commit();
                break;


        }
    }
}
```

메뉴 버튼이 클릭되면 `setOnNavigationItemSelectedListener()` 메소드를 통해 `SetFrag()` 메소드가 해당하는 `Fragment`로 교체한다.

## 실행 결과

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Android/BottomNavi/gif.gif?raw=true)


## 참고 자료

[https://youtu.be/stwCk_f3sCw](https://youtu.be/stwCk_f3sCw)