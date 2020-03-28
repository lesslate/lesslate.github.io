---
title: "PlayerPrefs 배열저장"
categories: 
  - Unity
last_modified_at: 2020-03-27T13:00:00+09:00
tags: 
  - Unity 
  - C#
toc: true
sidebar_main: true
---

## Intro

> PlayerPrefs에 배열저장하기


## 예제

> 스크립트

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class arraytest : MonoBehaviour
{

    void Start()
    {
    
////// 저장하기

        int[] number = new int[100]; // 정수형 배열 생성

        number[2] = 1;

        string strArr = ""; // 문자열 생성

        for (int i = 0; i < number.Length; i++) // 배열과 ','를 번갈아가며 tempStr에 저장
        {
            strArr = strArr + number[i];
            if (i < number.Length - 1) // 최대 길이의 -1까지만 ,를 저장
            {
                strArr = strArr + ",";
            }
        }

        print(strArr); // 0,0,1,0,0....으로 저장된 strArr

        PlayerPrefs.SetString("Data", strArr); // PlyerPrefs에 문자열 형태로 저장


////// 불러오기

        string[] dataArr = PlayerPrefs.GetString("Data").Split(','); // PlayerPrefs에서 불러온 값을 Split 함수를 통해 문자열의 ,로 구분하여 배열에 저장


        int[] number2 = new int[dataArr.Length]; // 문자열 배열의 크기만큼 정수형 배열 생성

        for (int i = 0; i < dataArr.Length; i++)
        {
            number2[i] = System.Convert.ToInt32(dataArr[i]); // 문자열 형태로 저장된 값을 정수형으로 변환후 저장
            print(number2[i]);
        }



    }


}
```

