---
layout: default
title: Blog
permalink: /blog/
---

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 1.5rem;">
      <code>{{ post.date | date: "%b %d, %Y" }}</code>  |
      <a href="{{ post.url }}"><strong>{{ post.title }}</strong></a><br>
      <small>{{ post.excerpt | markdownify | remove: '<p>' | remove: '</p>' | strip }}</small>
    </li>
  {% endfor %}
</ul>
