---
layout: default
title: Blog
permalink: /blog/
---

# Blog Posts

Here are some posts where I share my personal experiences.

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 1.5rem;">
      <em>{{ post.date | date: "%b %d, %Y" }}</em> |
      <a href="{{ post.url }}"><strong>{{ post.title }}</strong></a><br>
      <small>{{ post.excerpt }}</small>
    </li>
  {% endfor %}
</ul>
