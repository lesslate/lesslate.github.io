---
title: "메인 Categories 추가"
categories: 
  - Blogging
last_modified_at: 2019-02-04T13:00:00+09:00
tags: 
  - blogging 
toc: true
sidebar_main: true
---

## Intro

> - 메인 Categories 추가

## _includes/nav_list_main 파일 추가


**추가**

<script src="https://gist.github.com/lesslate/bbd03fd531e5eba8407185b4d7904bf6.js"></script>

카테고리들과 태그들을 읽어서 보여주고 클릭시 토글기능 추가



## _includes/script.html 수정

**추가**

<script src="https://gist.github.com/lesslate/2b5a33e9c099f3891f0e720c237d05a8.js"></script>

클릭시 flag 값 변경으로 토글



## _includes/sidebar.html 수정

**추가**

<script src="https://gist.github.com/lesslate/e12edb6f6a1978acd33db0cca37dc0b7.js"></script>

sidebar_main 이라는 변수가 있으면

nav_list_main을 불러오게됨


## 카테고리 추가

카테고리를 표시하고 싶은 페이지마다

 ``[sidebar_main: true]``를 추가




## 참고문서

[commit](https://github.com/lesslate/lesslate.github.io/commit/1369105ee344f682ac53525c02f9393e040eab2c)

[참고 블로그](https://imreplay.com/)