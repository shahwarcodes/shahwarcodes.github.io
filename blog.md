---
layout: page
title: Writing
---

I write about backend systems, ML platforms, and engineering lessons.

{% if site.posts.size > 0 %}
<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-item">
      <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
      <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
      {% if post.excerpt %}
      <div class="post-excerpt">{{ post.excerpt }}</div>
      {% endif %}
    </li>
  {% endfor %}
</ul>
{% else %}
<p>No posts yet. Check back soon!</p>
{% endif %}
