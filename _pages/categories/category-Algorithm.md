---
layout: archive
permalink: /categories/Algorithm
title: "Post about Algorithm."
author_profile: true
sidebar_main: true
search : false
---
<!-- 사이드바 카테고리 클릭 후 나오는 포스트 목록 정렬 변경 원래는 sort:"date"였음 --->
{% assign posts = site.categories.Algorithm | sort | reverse %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}


