---
layout: page
title: "About"
permalink: /about/
---

A blog focusing on data engineering and AI.

## Pages
<pre>
{%- assign urls = "" | split: "" -%}

{%- comment -%}Collect page URLs{%- endcomment -%}
{%- for p in site.pages -%}
  {%- if p.url and p.url != "/sitemap.xml" and p.url != page.url and p.url != "/404.html" and p.sitemap != false -%}
    {%- assign urls = urls | push: p.url -%}
  {%- endif -%}
{%- endfor -%}

{%- comment -%}Collect post URLs{%- endcomment -%}
{%- for post in site.posts -%}
  {%- if post.url and post.sitemap != false -%}
    {%- assign urls = urls | push: post.url -%}
  {%- endif -%}
{%- endfor -%}

{%- assign urls = urls | uniq | sort -%}

/
{%- assign prev_parts = "" | split: "" -%}
{%- assign prev_eff = 0 -%}

{%- for u in urls -%}
  {%- if u == "/" -%}{%- continue -%}{%- endif -%}

  {%- assign clean = u | remove_first: "/" -%}
  {%- assign parts = clean | split: "/" -%}

  {%- assign trailing_slash = false -%}
  {%- if parts.size > 0 and parts | last == "" -%}
    {%- assign trailing_slash = true -%}
    {%- assign eff = parts.size | minus: 1 -%}
  {%- else -%}
    {%- assign eff = parts.size -%}
  {%- endif -%}

  {%- assign min_eff = eff -%}
  {%- if prev_eff < min_eff -%}{%- assign min_eff = prev_eff -%}{%- endif -%}

  {%- assign common = 0 -%}
  {%- if min_eff > 0 -%}
    {%- assign max_i = min_eff | minus: 1 -%}
    {%- for i in (0..max_i) -%}
      {%- if parts[i] == prev_parts[i] -%}
        {%- assign common = common | plus: 1 -%}
      {%- else -%}
        {%- break -%}
      {%- endif -%}
    {%- endfor -%}
  {%- endif -%}

  {%- assign last_index = eff | minus: 1 -%}

  {%- for j in (common..last_index) -%}
    {%- capture indent -%}
      {%- if j > 0 -%}
        {%- for k in (1..j) -%}│   {%- endfor -%}
      {%- endif -%}
    {%- endcapture -%}

    {%- assign seg = parts[j] -%}

    {%- comment -%}
      Append "/" to intermediate nodes; also append "/" to leaf if original URL ended in "/"
    {%- endcomment -%}
    {%- if j < last_index -%}
{{ indent }}├── {{ seg }}/
    {%- else -%}
      {%- if trailing_slash -%}
{{ indent }}└── {{ seg }}/
      {%- else -%}
{{ indent }}└── {{ seg }}
      {%- endif -%}
    {%- endif -%}
  {%- endfor -%}

  {%- assign prev_parts = parts -%}
  {%- assign prev_eff = eff -%}
{%- endfor -%}
</pre>