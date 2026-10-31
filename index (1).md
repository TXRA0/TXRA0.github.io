---
title: "Bot Design"
permalink: /bot-design/
layout: archive
classes: wide
---

Architecture, interfaces, state management, decision-making, and the trade-offs involved in keeping a Screeps bot understandable as it grows.

{% assign section_posts = site.categories.bot-design %}
{% if section_posts and section_posts.size > 0 %}
{% for post in section_posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

{{ post.excerpt | strip_html | truncate: 240 }}

<small>{{ post.date | date: "%d %B %Y" }}</small>
{% endfor %}
{% else %}
_No bot-design articles published yet._
{% endif %}
