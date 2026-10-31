---
title: "Research"
permalink: /research/
layout: archive
classes: wide
---

Experiments, hypotheses, measurement notes, and post-mortems. Research posts should make it clear what was tested, what evidence was collected, and what conclusions are still uncertain.

{% assign section_posts = site.categories.research %}
{% if section_posts and section_posts.size > 0 %}
{% for post in section_posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

{{ post.excerpt | strip_html | truncate: 240 }}

<small>{{ post.date | date: "%d %B %Y" }}</small>
{% endfor %}
{% else %}
_No research notes published yet._
{% endif %}
