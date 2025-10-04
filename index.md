---
layout: default
title: Home
---

# 🌈 Welcome to My DevOps Blog

Hi, I’m **Dheeraj Singh**, a DevOps Engineer passionate about CI/CD, Cloud, and Automation.

This blog covers:
- 🐳 Docker
- ☸️ Kubernetes
- ☁️ AWS
- ⚙️ Jenkins
- 💡 Terraform

![DevOps Banner](assets/images/banner.jpg)

---

## 🆕 All Blog Posts

{% for post in site.posts %}
### [{{ post.title }}]({{ post.url | relative_url }})
📅 {{ post.date | date: "%B %d, %Y" }}

{{ post.excerpt }}

---
{% endfor %}

