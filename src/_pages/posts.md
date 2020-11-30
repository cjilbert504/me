---
layout: page
title: Posts
permalink: /posts/
---

<div class="container">
<ul id="posts-list">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
</div>