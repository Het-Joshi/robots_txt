---
layout: default
title: Library
permalink: /library/
---

# Library

<ul>
{% for post in site.categories.posts %}
  <li>
    <h2>{{ post.title }}</h2>
    <p>{{ post.description }}</p>
    <p>{{ post.excerpt }}</p>
    <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">Read more</a>
  </li>
{% endfor %}
</ul>
