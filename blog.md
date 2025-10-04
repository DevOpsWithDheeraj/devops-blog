---
layout: default
title: Blog
---

# 📰 DevOps Blog Posts

{% for post in site.posts %}
### [{{ post.title }}]({{ https://github.com/DevOpsWithDheeraj/devops-blog/blob/main/_posts/ }})
📅 *{{ post.date | date: "%B %d, %Y" }}*

{{ post.excerpt }}
---

{% endfor %}
