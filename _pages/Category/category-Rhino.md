---
title: "Post about Rhino"
layout: archive
permalink: /categories/rhino
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Rhino | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
