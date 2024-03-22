---
layout: categories
category: code
title: code posts
permalink: /categories/code/
---

<ul>
{% for post in site.posts %}
  {% if post.categories contains 'code' %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>