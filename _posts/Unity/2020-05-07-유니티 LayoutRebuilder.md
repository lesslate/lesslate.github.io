---
title: "유니티 LayoutRebuilder"
categories: 
  - Unity
last_modified_at: 2020-05-07T13:00:00+09:00
tags: 
  - Unity 
  - C#
toc: true
sidebar_main: true
---

## Intro

> LayoutRebuilder를 통한 Content Size Filter 버그 해결 


## 레이아웃 버그

![1](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unity/layoutRebuilder/11.png?raw=true)

레이아웃의 자식으로 `Content Size Filter`를 가진 `Text` 오브젝트를 넣어 텍스트 길이에 따라 유연하게 배치되도록 했지만 
비활성화 상태에서 텍스트 변경후 다시 활성화될때 위와같이 위치가 망가져 버렸다.

이를 해결하기위해 재활성화시 `LayoutRebuilder.ForceRebuildLayoutImmediate` 함수를 사용하여 레이아웃을 재구성하여 해결했다.

## 스크립트

```c#
LayoutRebuilder.ForceRebuildLayoutImmediate(레이아웃.GetComponent<RectTransform>()); //레이아웃 refresh
```

## 결과

![2](https://github.com/lesslate/lesslate.github.io/blob/master/assets/img/Unity/layoutRebuilder/2.png?raw=true)


## 참고

[https://docs.unity3d.com/2018.1/Documentation/ScriptReference/UI.LayoutRebuilder.ForceRebuildLayoutImmediate.html](https://docs.unity3d.com/2018.1/Documentation/ScriptReference/UI.LayoutRebuilder.ForceRebuildLayoutImmediate.html)