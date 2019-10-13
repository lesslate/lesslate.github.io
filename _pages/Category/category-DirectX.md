---
title: "Post about DirectX"
layout: archive
permalink: /categories/directx
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.DirectX | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
