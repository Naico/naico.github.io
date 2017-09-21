---
layout: default
---

<ul class="blog-list">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{post.date}} - {{ post.title }}</a>
    </li>
  {% endfor %}
</ul>