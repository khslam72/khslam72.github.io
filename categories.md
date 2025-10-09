---
layout: default
title: Categories
permalink: /categories/
---

<div class="post-content-area">
  <header class="post-header">
    <h1 class="post-title">Categories</h1>
  </header>
  
  <div class="post-body">

    <!-- ✅ 1. 카테고리 인덱스 (빠른 이동 메뉴) -->
    <div class="category-index-container">
      <h3>Category Index</h3>
      <ul class="category-index">
        {% assign categories = "" %}
        {% for post in site.posts %}
          {% for category in post.categories %}
            {% assign categories = categories | append: category | append: "||" %}
          {% endfor %}
        {% endfor %}
        {% assign category_list = categories | split: "||" | uniq | sort %}

        {% for category_name in category_list %}
          {% if category_name == "" %}{% continue %}{% endif %}
          <li class="index-item">
            <a href="#{{ category_name | slugify }}">{{ category_name }}</a>
          </li>
        {% endfor %}
      </ul>
    </div>

    <!-- ✅ 2. 카테고리 목록 (다중 칼럼) -->
    <div class="category-archive-grid">
      {% for category_name in category_list %}
        {% if category_name == "" %}{% continue %}{% endif %}
        <div class="category-group">
          <h2 class="category-name" id="{{ category_name | slugify }}">{{ category_name }}</h2>
          <ul class="category-post-list">
            {% for post in site.posts %}
              {% if post.categories contains category_name %}
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
