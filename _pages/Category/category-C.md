---
title: "Post about C Programming"
layout: archive
permalink: /categories/CProgramming
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.CProgramming | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}

