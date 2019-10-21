---
title: "Post about AI"
layout: archive
permalink: /categories/AI
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.ai | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
