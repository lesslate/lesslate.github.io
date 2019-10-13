---
title: "Post about DesignPattern"
layout: archive
permalink: /categories/designpattern
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.DesignPattern | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
