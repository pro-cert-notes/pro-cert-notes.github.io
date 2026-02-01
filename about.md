---
layout: page
title: "About"
permalink: /about/
---

A blog focusing on data engineering and AI.

## Sitemap
<pre>
/&#10;
{% assign page_urls = site.pages | map: "url" %}
{% assign post_urls = site.posts | map: "url" %}
{% assign urls = page_urls | concat: post_urls | uniq | sort %}

{% for u in urls %}
  {% unless u == "/" or u == page.url or u == "/sitemap.xml" or u == "/feed.xml" or u contains "/assets/" %}
    {% assign parts = u | split:'/' %}
    {% assign depth = parts.size | minus: 3 %}
    {% if depth < 0 %}{% assign depth = 0 %}{% endif %}

    {% capture indent %}{% for i in (1..depth) %}│  {% endfor %}{% endcapture %}
{{ indent }}├─ {{ u }}&#10;
  {% endunless %}
{% endfor %}
</pre>