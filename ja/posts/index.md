---
layout: posts
title:  📜 ブログ記事まとめ
thumbnail: bg-sky.jpg
---

<ul style="list-style: none; padding-top: 10px; padding-bottom: 70px;">
  {% assign max_related = 10000 %}
  {% assign min_common_tags = 0 %}
  {% assign max_related_counter = 0 %}

  {% for post in site.posts %}
    {% assign same_tag_count = 0 %}
    {% for tag in post.tags %}
      {% if post.url != page.url %}
        {% if page.tags contains tag %}
          {% assign same_tag_count = same_tag_count | plus: 1 %}
        {% endif %}
      {% endif %}
    {% endfor %}

    {% if same_tag_count >= min_common_tags %}
      {% include recent_post.html %}
      {% assign max_related_counter = max_related_counter | plus: 1 %}
      {% if max_related_counter >= max_related %}
        {% break %}
      {% endif %}
    {% endif %}
  {% endfor %}
</ul>

<hr>

{% include recent_tweets.html %}
