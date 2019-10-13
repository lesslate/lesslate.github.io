---
title: "Post about Mathematics"
layout: archive
permalink: /categories/mathematics
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Mathematics | sort:"title" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
