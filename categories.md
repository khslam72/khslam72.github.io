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

      {%- comment -%}
      1) 모든 포스트의 카테고리를 수집
      2) JSON 첫 글자로 타입 판별:
         - 문자열 => cat_json 첫 글자: "
         - 객체   => 첫 글자: {
         - 배열   => 첫 글자: [
      3) 문자열만 합쳐 uniq/sort
      {%- endcomment -%}
      {% assign categories_concat = "" %}
      {% for post in site.posts %}
        {% if post.categories %}
          {% for cat in post.categories %}
            {% assign cat_json = cat | jsonify %}
            {% assign first_char = cat_json | slice: 0, 1 %}
            {% if first_char == '"' %}
              {% assign cat_clean = cat | strip %}
              {% unless cat_clean == "" %}
                {% assign categories_concat = categories_concat | append: cat_clean | append: "||" %}
              {% endunless %}
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}
      {% assign category_list = categories_concat | split: "||" | uniq | sort %}

      {%- comment -%}
      카테고리별 포스트 목록 출력 (최신순)
      {%- endcomment -%}
      {% for category_name in category_list %}
        {% assign cat = category_name | strip %}
        {% if cat == "" %}{% continue %}{% endif %}

        <div class="category-group">
          <h2 class="category-name" id="{{ cat | slugify }}">{{ cat }}</h2>

          {% assign posts_in_cat = site.posts | where_exp: "p", "p.categories contains cat" %}
          {% if posts_in_cat and posts_in_cat != empty %}
            <ul class="category-post-list">
              {% for post in posts_in_cat %}
                <li>
                  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                  <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
                </li>
              {% endfor %}
            </ul>
          {% else %}
            <p><em>No posts in “{{ cat }}”.</em></p>
          {% endif %}
        </div>
      {% endfor %}

    </div>
  </div>
</div>
