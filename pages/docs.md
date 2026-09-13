---
title: Docs
permalink: /docs/
nav_exclude: true
---

# Documentation

A knowledge base of short how-to articles, commands, and troubleshooting notes I've
collected over the years. Use the search box (top left) or the **Docs** folder in the
side navigation to find a topic.

{% assign docs = site.docs | sort: 'title' %}
<ul>
{% for doc in docs %}
  <li><a href="{{ doc.url | prepend: site.baseurl }}">{{ doc.title }}</a></li>
{% endfor %}
</ul>