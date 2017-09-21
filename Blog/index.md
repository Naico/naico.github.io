---
layout: default
title: Kun Wang - Blog
category: blog
---


<!-- -------------------------------------------------------------- -->
<!-- Two tab pages for classification ----------------------------- -->
<!-- -------------------------------------------------------------- -->
<div class="row">
<a class="button btn-primary" href="/blog/index.html">By year</a>
<a class="button btn-primary" href="/blog/categories.html">By categories</a>
</div>

<!-- -------------------------------------------------------------- -->
<!-- Collection of Nice Blogs ------------------------------------- -->
<!-- -------------------------------------------------------------- -->
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

<br>
<!-- -------------------------------------------------------------- -->
<!-- Collection of Nice Blogs ------------------------------------- -->
<!-- -------------------------------------------------------------- -->
<!-- <section class="inner">
<hr>
<h3>Blogroll</h3><a name="blogs"></a>
<ul>
{% for piece in site.data.blogSites %}
  <div>
    <li> 
	    <p><a href="{{ piece.url }}"><strong><i>{{ piece.title }}</i></strong></a>, 
	    {{ piece.creator }}, {{ piece.description }}
	</li>
  </div>
{% endfor %}
</ul>
<p>[<a href="#top" target="_self"><i>go top</i></a>]</p>
</section> -->
<!-- <br> -->
<!-- -------------------------------------------------------------- -->
<!-- My famous quotes --------------------------------------------- -->
<!-- -------------------------------------------------------------- -->
<section class="inner">
<hr>
<h3>On Quantum Computation</h3><a name="blogs"></a>

{% for piece in site.data.quotations %}
<blockquote>
	<p>{{ piece.content }}<span style="float:right">- {{ piece.creator }}</span></p>
</blockquote>
{% endfor %}

  <p>[<a href="#top" target="_self"><i>go top</i></a>]</p>
</section>
