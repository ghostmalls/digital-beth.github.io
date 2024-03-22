---
layout: categories
category: photos
title: photos
permalink: /categories/photos/
---

<ul>
{% for post in site.posts %}
  {% if post.categories contains 'photos' %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>