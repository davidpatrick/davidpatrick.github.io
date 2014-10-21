---
layout: page
title: Archives
permalink: /archives/
---

{% for post in site.posts  limit: 50 %}
  {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}