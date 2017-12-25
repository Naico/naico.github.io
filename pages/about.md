---
layout: page
title: About
description: Naico的后花园
keywords: Naico
menu: 关于
permalink: /about/
---

Naico Wang
生活在上海的底层码农。
Live for coding...

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
