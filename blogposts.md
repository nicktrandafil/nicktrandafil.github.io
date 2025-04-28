---
layout: default
title: Blogposts
permalink: /blogposts/
---

# Blog Posts

<ul>
  {% for post in site.posts %}
    <li style="margin-bottom: 1.5rem;">
      <a href="{{ post.url }}"><strong>{{ post.title }}</strong></a><br>
      <small>{{ post.excerpt }}</small>
    </li>
  {% endfor %}
</ul>
