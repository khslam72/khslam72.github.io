---
layout: default
title: Search
permalink: /search/
---

<div class="post-content-area">
  <header class="post-header">
    <h1 class="post-title">Search</h1>
  </header>
  
  <div class="post-body">
    <div class="search-container">
      <input type="text" id="search-input" placeholder="Search for artists, songs, and more...">
      <ul id="search-results"></ul>
    </div>
  </div>
</div>

<!-- 검색 기능을 위한 스크립트 (이 페이지에서만 로드) -->
<script src="https://unpkg.com/simple-jekyll-search@1.10.0/dest/simple-jekyll-search.min.js"></script>
<script>
  var sjs = SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('search-results'),
    json: '/search.json',
    searchResultTemplate: '<li class="search-result-item"><a href="{url}"><h4>{title}</h4><p>{excerpt}</p><span class="search-result-date">{date}</span></a></li>',
    noResultsText: '<li>No results found.</li>',
    limit: 10,
    fuzzy: false
  });
</script>
