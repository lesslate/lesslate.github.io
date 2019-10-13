---
title: "Post about Android"
layout: archive
permalink: /categories/android
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Android | sort:"title" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
