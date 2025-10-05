---
layout: default
title: Blog
permalink: /blog/
---

# 📰 DevOps Blog Posts

{% for post in site.posts %}
<div class="post-preview">
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  <span class="post-date">📅 {{ post.date | date: "%B %d, %Y" }}</span>
  <p>{{ post.excerpt | strip_html | truncate: 200 }}</p>
</div>
{% endfor %}

