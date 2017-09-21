---
layout: default
title: Naico
category: blog
---


<section class="inner">
  <ul class="posts">
    {% for post in site.posts %}
	  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
	  {% if year != y %}
		{% assign year = y %}
		<h3><li class="listing-seperator">{{ y }}</li></h3>
	  {% endif %}
	  <li class="listing-item">
		<time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
		<a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
	  </li>
    {% endfor %}
  </ul>
  <p>[<a href="#top" target="_self"><i>go top</i></a>]</p>
</section>

