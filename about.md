---
layout: page
title: "About"
permalink: /about/
---

A blog focusing on data engineering and AI.

## Sitemap
<style>
  .sitemap-ascii .line{
    white-space: pre;              /* preserve ASCII indentation */
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace;
    line-height: 1.25;             /* tighter lines */
    margin: 0;                     /* remove vertical gaps */
    padding: 0;
  }
  .sitemap-ascii .path{
    opacity: .65;
    font-size: .9em;
    margin-left: .5em;
  }
</style>
<div class="sitemap-ascii">
  <div class="line">└─ <a href="{{ '/' | relative_url }}">/</a></div>

  {%- assign pages = site.pages | sort: "url" -%}
  {%- for p in pages -%}
    {%- if p.url
      and p.url != "/"
      and p.url != page.url
      and p.url != "/sitemap.xml"
      and p.url != "/feed.xml"
      and p.sitemap != false
      and p.title
    -%}
      {%- assign depth = p.url | split:'/' | size | minus: 2 -%}
      {%- if depth < 0 -%}{%- assign depth = 0 -%}{%- endif -%}
      {%- capture indent -%}{%- for i in (1..depth) -%}│  {%- endfor -%}{%- endcapture -%}
      <div class="line">{{ indent }}├─ <a href="{{ p.url | relative_url }}">{{ p.title | escape }}</a> <span class="path">{{ p.url }}</span></div>
    {%- endif -%}
  {%- endfor -%}

  {%- assign posts = site.posts | sort: "url" -%}
  {%- for post in posts -%}
    {%- if post.url and post.sitemap != false -%}
      {%- assign depth = post.url | split:'/' | size | minus: 2 -%}
      {%- if depth < 0 -%}{%- assign depth = 0 -%}{%- endif -%}
      {%- capture indent -%}{%- for i in (1..depth) -%}│  {%- endfor -%}{%- endcapture -%}
      <div class="line">{{ indent }}├─ <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a> <span class="path">{{ post.url }}</span></div>
    {%- endif -%}
  {%- endfor -%}
</div>