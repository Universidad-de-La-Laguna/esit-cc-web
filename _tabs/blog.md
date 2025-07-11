---
title: Blog
icon: fas fa-rss
order: 2
layout: page
---

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}