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
```
<nav class="nav__list">
  <input id="ac-toc" name="accordion-toc" type="checkbox" />
  <label for="ac-toc">{{ site.data.ui-text[site.locale].menu_label | default: "Toggle Menu" }}</label>
  <ul class="nav__items" id="category_tag_menu">
      <li>
        <span class="nav__sub-title" v-on:click='togglec()'>Categories</span>
        <ul v-show="flag_c">
        {% for category in site.categories %}
           <li><a href="/categories/{{category[0] | slugify}}" class="">{{category[0] | capitalize}} ({{category[1].size}})</a></li>
        {% endfor %}
        </ul>
        
        <span class="nav__sub-title" v-on:click='togglet()'>tags</span>
        <ul v-show="flag_t">
        {% for tag in site.tags %}
           <li><a href="/tags/#{{tag[0] | slugify}}" class="">{{tag[0] | capitalize }} ({{tag[1].size}})</a></li>
        {% endfor %}
        </ul>
        
      </li>
    
  </ul>
</nav>
```

카테고리들과 태그들을 읽어서 보여주고 클릭시 토글기능 추가



## _includes/script.html 수정

**추가**
```
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
 <script>
  new Vue({
    el : '#category_tag_menu',
    data : {
      flag_c : true,
      flag_t : false
    },
    methods : {
      togglec: function(){
        this.flag_c = !this.flag_c;
      },
      togglet: function(){
        this.flag_t = !this.flag_t;
      }
    }
  });
 </script> 
```

클릭시 flag 값 변경으로 토글



## _includes/sidebar.html 수정

**추가**
```
{% if page.sidebar_main %}
    {% include nav_list_main %}
  {% endif %}
```

sidebar_main 이라는 변수가 있으면

nav_list_main을 불러오게됨


## 카테고리 추가

카테고리를 표시하고 싶은 페이지마다

 ``[sidebar_main: true]``를 추가




## 참고문서

[commit](https://github.com/lesslate/lesslate.github.io/commit/1369105ee344f682ac53525c02f9393e040eab2c)

[참고 블로그](https://imreplay.com/)