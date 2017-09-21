---
layout: default
---
# Article List

<ul class="blog-list">
  {% for post in site.posts %}
    <li>
      <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
       - 
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
