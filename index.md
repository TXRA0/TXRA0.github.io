---
title: "Battle Reports"
permalink: /battle-reports/
layout: archive
classes: wide
---

Battle reports turn matches into engineering feedback. Each report should describe the situation, the bot version, the observed behaviour, the result, and the changes worth testing next.

{% assign section_posts = site.categories.battle-reports %}
{% if section_posts and section_posts.size > 0 %}
{% for post in section_posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

{{ post.excerpt | strip_html | truncate: 240 }}

<small>{{ post.date | date: "%d %B %Y" }}</small>
{% endfor %}
{% else %}
_No battle reports published yet. Add match notes when you have a useful lesson to share._
{% endif %}
