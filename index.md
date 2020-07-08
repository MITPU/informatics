---
layout: default
---

<div class="home">

  <ul class="post-list">

    {% assign posts_grouped_by_category = site.posts | group_by:'category' %}
    {% for post_group in posts_grouped_by_category %}
      <li class='post-category'>{{ post_group.name | capitalize }}</li>
      {% for post in post_group.items %}
        <li class='post'>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
          <span class="post-meta date-author">{{ post.author | capitalize}} | {{ post.date | date: "%Y-%m-%d" }}</span>
        </li>
      {% endfor %}
    {% endfor %}
  </ul>

</div>
