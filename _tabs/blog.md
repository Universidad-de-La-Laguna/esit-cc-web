---
title: blog
icon: fas fa-rss
order: 5
layout: page
---

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}