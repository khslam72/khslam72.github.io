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
      <!-- ✅ 'site.categories | sort' 를 'sorted_categories' 라는 변수에 저장 -->
      {% assign sorted_categories = site.categories | sort %}
      
      <!-- ✅ 'sorted_categories' 변수를 사용하도록 수정 -->
      {% for category in sorted_categories %}
        <div class="category-group">
          <h2 class="category-name" id="{{ category | first | slugify }}">{{ category | first }}</h2>
          <ul class="category-post-list">
            {% for post in category.last %}
              <li>
                <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
              </li>
            {% endfor %}
          </ul>
        </div>
      {% endfor %}
    </div>
  </div>
</div>
