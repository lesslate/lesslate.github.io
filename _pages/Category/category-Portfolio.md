---
title: "Post about Portfolio"
layout: archive
permalink: /categories/portfolio
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.portfolio | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
