---
title: "Guides"
permalink: /guides/
layout: archive
classes: wide
---

Step-by-step explanations of Screeps programming concepts and combat systems. Guides aim to explain the problem, the design choices, the implementation, and how to test the result.

{% assign section_posts = site.categories.guides %}
{% if section_posts and section_posts.size > 0 %}
{% for post in section_posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

{{ post.excerpt | strip_html | truncate: 240 }}

<small>{{ post.date | date: "%d %B %Y" }}</small>
{% endfor %}
{% else %}
_No guides published yet. The first guide is on its way._
{% endif %}
