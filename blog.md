---
layout: default
title: Blog
permalink: /blog/
---

# Blog

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 1.5rem;">
      <code>{{ post.date | date: "%b %d, %Y" }}</code>  |
      <a href="{{ post.url }}"><strong>{{ post.title }}</strong></a><br>
      <small>{{ post.excerpt }}</small>
    </li>
  {% endfor %}
</ul>
