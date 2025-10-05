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
    <div class="category-archive">
      
      <!-- ✅ 모든 카테고리를 안전하게 수집하고 정렬하는 새로운 코드 -->
      {% assign all_categories = "" %}
      {% for post in site.posts %}
        {% for category in post.categories %}
          {% assign all_categories = all_categories | append: category | append: "||" %}
        {% endfor %}
      {% endfor %}
      {% assign category_list = all_categories | split: "||" | uniq | sort %}

      <!-- ✅ 정제된 카테고리 목록을 사용 -->
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
