---
layout: categories
category: python
title: python posts
permalink: /categories/python/
---

<ul>
{% for post in site.posts %}
  {% if post.categories contains 'python' %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>