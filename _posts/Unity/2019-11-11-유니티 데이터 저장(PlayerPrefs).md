---
title: "유니티 데이터 저장(PlayerPrefs)"
categories: 
  - Unity
last_modified_at: 2019-11-11T13:00:00+09:00
tags: 
  - Unity 
  - C#
toc: true
sidebar_main: true
---

## Intro

> 데이터 저장(PlayerPrefs)

## PlayerPrefs

`PlayerPrefs`는 유니티에서 제공하는 클래스로 간단한 데이터를 저장할 수 있다. 

## DataManager


```c#
public class DataManager : MonoBehaviour

{
    public static DataManager instance
    {
        get
        {
            
            if (m_instance == null)
            {          
                m_instance = FindObjectOfType<DataManager>();
            }
            return m_instance;
        }
    }

    private static DataManager m_instance; 
    
    
    public long crystal
    {
        get
        {
            if (!PlayerPrefs.HasKey("Crystal")) // 키 값이 없을때 기본 값 0 리턴
            {
                return 0;
            }
            return long.Parse(PlayerPrefs.GetString("Crystal"));
        }
        set
        {
            PlayerPrefs.SetString("Crystal", value.ToString());
            
        }
    }
```

데이터를 관리하는 `DataManger` 클래스를 만들고 싱글턴으로 만들어주었다.

게임에 사용될 화폐인 crystal을 프로퍼티를 이용해 읽거나 쓸수있게 했으며 `PlayerPrefs`를 이용해 `Crystal`이라는 `Key`에 데이터를 저장하도록 했다. 이때 `PlayerPrefs`는 `float, int, string` 만 저장할 수 있으므로 `long`타입인 crystal은 저장할 때는 `string`형으로 불러올 땐 `string`형을 `long`으로 `parse` 하도록 했다.


> 데이터 변경

```c#
DataManager.instance.crystal += reward;
InGameUIManager.instance.UpdateCrystal(DataManager.instance.crystal);
```

몬스터가 죽을 때 crystal의 수치를 증가하도록 했다.

```c#
UpdateCrystal(DataManager.instance.crystal);
```

`UIManager`는 저장된 데이터를 불러와 갱신시키게 했다.

## 실행결과

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unity/playerprefs/1.png?raw=true)

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unity/playerprefs/2.png?raw=true)

몬스터를 잡으면 크리스탈이 증가하며 게임을 껐다 켜도 저장된 값이 그대로 있다.

## 참고자료

