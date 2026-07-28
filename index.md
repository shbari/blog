---
layout: home
title: Latest Articles
---

Welcome to my space! I write about hydrology research, climate systems, coding, and navigating life here in Japan.

## Recent Posts
{% for post in site.posts %}
* **{{ post.date | date: "%B %d, %Y" }}** — [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}
