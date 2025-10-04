---
layout: default
title: Home
---

# 🌈 Welcome to My DevOps Blog

Hi, I’m **Dheeraj Singh**, a DevOps Engineer passionate about CI/CD, Cloud, and Automation.

This blog covers everything from:
- 🐳 Docker
- ☸️ Kubernetes
- ☁️ AWS
- ⚙️ Jenkins
- 💡 Terraform

![DevOps Banner](assets/images/banner.jpg)

> 💬 “Automate everything that can be automated!”

---

## 🆕 Latest Posts

{% for post in site.posts limit:3 %}
### [{{ post.title }}]({{ post.url | relative_url }})
📅 {{ post.date | date: "%b %d, %Y" }}
{{ post.excerpt }}
---

{% endfor %}

