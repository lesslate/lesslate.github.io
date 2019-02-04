---
title: "Back to top 버튼 추가"
categories: 
  - Unreal4
last_modified_at: 2019-02-04T13:00:00+09:00
tags: 
  - blogging 
toc: true
sidebar_main: true
---

## Intro

> - Back to Top 버튼 추가

## _sidebar.scss 수정


**추가**
```
.sidebar__top {
  position: fixed;
  bottom: 1.5em;
  right: 2em;
  z-index: 10;
}
```

## default.html 수정

**추가**
```
<aside class="sidebar__top">
<a href="#site-nav"> <i class="fas fa-angle-double-up fa-2x"></i></a>
</aside>
```


## 참고문서

[commit](https://github.com/lesslate/lesslate.github.io/commit/ce2cccc83054c8d192f98a10f8a6a3af3e1d9a65)
[관련 문서](https://github.com/mmistakes/minimal-mistakes/issues/1731)