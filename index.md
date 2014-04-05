---
layout: page
title: sudo su
tagline: Supporting tagline
---
{% include JB/setup %}
## Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}: {{ post.description }}</a></li>
  {% endfor %}
</ul>

## Blog Setup Documentation
Read [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

