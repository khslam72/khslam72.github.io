---
layout: default
title: Tags
permalink: /tags/
---

<div class="post-content-area">
  <header class="post-header">
    <h1 class="post-title">Tags</h1>
  </header>
  
  <div class="post-body">

    <!-- 1. 태그 인덱스 (빠른 이동 메뉴) -->
    <div class="tag-index-container">
      <h3>Tag Index</h3>
      <ul class="tag-index">
        {% assign all_tags = "" %}
        {% for post in site.posts %}
          {% for tag in post.tags %}
            {% assign all_tags = all_tags | append: tag | append: "||" %}
          {% endfor %}
        {% endfor %}
        {% assign tag_list = all_tags | split: "||" | uniq | sort %}

        {% for tag_name in tag_list %}
          {% if tag_name == "" %}{% continue %}{% endif %}
          <li class="index-item">
            <a href="#{{ tag_name | slugify }}">{{ tag_name }}</a>
          </li>
        {% endfor %}
      </ul>
    </div>

    <!-- 2. 태그 목록 -->
    <div class="tag-archive">
      {% for tag_name in tag_list %}
        {% if tag_name == "" %}{% continue %}{% endif %}
        <div class="tag-group">
          <h2 class="tag-name" id="{{ tag_name | slugify }}">{{ tag_name }}</h2>
          <ul class="tag-post-list">
            {% for post in site.posts %}
              {% if post.tags contains tag_name %}
                <li>
                  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                  <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
                </li>
              {% endif %}
            {% endfor %}
          </ul>
        </div>
      {% endfor %}
    </div>

  </div>
</div>
