---
layout: page
title: Home
---

<h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>

{%- if site.posts.size > 0 -%}
<ul class="post-list">
  {%- for post in site.posts -%}
    <li>
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      <span class="post-meta">{{ post.date | date: date_format }}</span>

      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>

      {%- if site.minima.show_excerpts -%}
        {{ post.excerpt }}
      {%- endif -%}
    </li>
  {%- endfor -%}
</ul>
{%- endif -%}

## Repositories

{%- assign repos = site.github.public_repositories
  | where_exp: "r", "r.fork == false"
  | where_exp: "r", "r.archived == false"
  | where_exp: "r", "r.disabled == false"
  | where_exp: "r", "r.name != site.github.repository_name"
  | sort: "pushed_at"
  | reverse
-%}

<ul class="repo-list">
  {%- for repo in repos -%}
    {%- assign owner = repo.owner.login -%}
    {%- assign branch = repo.default_branch | default: "main" -%}
    {%- capture zip_url -%}https://github.com/{{ owner }}/{{ repo.name }}/archive/refs/heads/{{ branch }}.zip{%- endcapture -%}

    <li class="repo-list-item">
      <a href="{{ repo.html_url }}">{{ repo.name }}</a>

      {%- if repo.description and repo.description != "" -%}
        <div class="repo-desc">{{ repo.description }}</div>
      {%- endif -%}

      <small class="repo-meta">
        {%- if repo.language %}{{ repo.language }} · {% endif %}Updated {{ repo.pushed_at | date: "%Y-%m-%d" }} · {% if repo.license and repo.license.spdx_id %}{{ repo.license.spdx_id }} · {% endif -%}
        <a href="{{ zip_url }}" rel="nofollow">Download</a>
      </small>
    </li>
  {%- endfor -%}
</ul>