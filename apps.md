---
layout: default
title: Apps
permalink: /apps/
---

# Apps

Here are some of the applications and projects I've built.

<ul>
  {% for app in site.apps %}
    <li style="margin-bottom: 1.5rem;">
      <a href="{{ app.url }}"><strong>{{ app.title }}</strong></a><br>
      <small>{{ app.excerpt }}</small>
    </li>
  {% endfor %}
</ul>
