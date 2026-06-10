---
layout: default
title: Library
permalink: /library/
---

<div class="wrap narrow library">
  <h1>Library</h1>
  <p class="sub">everything I've written, newest first.</p>

  <div class="searchbar">
    <span class="pmt">$ grep</span>
    <label for="search" class="skip">Search posts</label>
    <input type="text" id="search" onkeyup="filterPosts()" placeholder="filter posts…" autocomplete="off" />
  </div>

  <ul id="filtered-posts">
    {% for post in site.categories.posts %}
    <li class="post">
      <a href="{{ site.baseurl }}{{ post.url }}" style="display:block;">
        <div class="post-meta">
          {% for t in post.tags %}<span class="tag">#{{ t }}</span>{% endfor %}
          <span>{{ post.date | date: "%b %-d, %Y" }}</span>
        </div>
        <h3>{{ post.title }}</h3>
        <p class="desc">{{ post.description }}</p>
        <p class="exc" style="display:none;">{{ post.excerpt | strip_html }}</p>
      </a>
    </li>
    {% endfor %}
  </ul>
</div>

<script>
function filterPosts() {
  var q = document.getElementById('search').value.toLowerCase();
  document.querySelectorAll('#filtered-posts .post').forEach(function(post){
    var title = (post.querySelector('h3')||{}).textContent || '';
    var desc  = (post.querySelector('.desc')||{}).textContent || '';
    var exc   = (post.querySelector('.exc')||{}).textContent || '';
    var hay = (title + ' ' + desc + ' ' + exc).toLowerCase();
    post.style.display = hay.indexOf(q) > -1 ? '' : 'none';
  });
}
</script>
