---
title: "Post about TIL"
layout: archive
permalink: /categories/til
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.TIL | sort:"date" | reverse %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}