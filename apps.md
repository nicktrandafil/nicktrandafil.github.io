---
layout: default
title: Apps
permalink: /apps/
---

# Apps

Here are some of the applications I've built. For feature requests or support, just <a href="mailto:nicktrandafil@gmail.com">email me</a>.

<ul>
  {% for app in site.apps %}
    <li style="margin-bottom: 1.5rem;">
      <a href="{{ app.url }}"><strong>{{ app.title }}</strong></a><br>
      <small>{{ app.excerpt }}</small>
    </li>
  {% endfor %}
</ul>
