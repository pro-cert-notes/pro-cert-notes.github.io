---
layout: page
title: "About"
permalink: /about/
---

A blog focusing on data engineering and AI.

## Sitemap
<pre>
{% assign page_urls = site.pages | map: "url" %}
{% assign post_urls = site.posts | map: "url" %}
{% assign urls = page_urls | concat: post_urls | uniq | sort %}

{% for u in urls %}
  {% if u == "/sitemap.xml" or u == "/feed.xml" %}
    {% continue %}
  {% endif %}

  {% assign parts = u | remove_first:'/' | split:'/' %}
  {% assign depth = parts.size | minus: 1 %}

  {% capture indent %}
    {% for i in (1..depth) %}│  {% endfor %}
  {% endcapture %}

{{ indent }}├─ {{ u }}
{% endfor %}
</pre>