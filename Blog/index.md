---
layout: default
title: Blogs
---


<div class="case-studies-body">
	<ul class="listing">
		{% assign projects = site.posts | sort: 'listing-priority' %}
		{% for project in projects %}
		<li>
			<h2><a href="{{ project.url }}">{{ project.title }}</a></h2>
			{{ project.content }}
		</li>
		{% endfor %}
	</ul>
</div>

