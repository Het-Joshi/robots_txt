---
layout: default
title: Library
permalink: /library/
---

# Library

<!-- Search box for filtering posts -->
<label for="search">Search:</label>
<input type="text" id="search" onkeyup="filterPosts()">

<!-- Container for displaying filtered posts -->
<ul id="filtered-posts">
  {% for post in site.categories.posts %}
    <li class="post">
      <h2>{{ post.title }}</h2>
      <p>{{ post.description }}</p>
      <p>{{ post.excerpt }}</p>
      <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.description }}">Read more</a>
    </li>
  {% endfor %}
</ul>

<script>
function filterPosts() {
  const searchInput = document.getElementById('search').value.toLowerCase();
  const posts = document.querySelectorAll('.post');
  posts.forEach(post => {
    const title = post.querySelector('h2').textContent.toLowerCase();
    const description = post.querySelector('p:nth-of-type(1)').textContent.toLowerCase();
    const excerpt = post.querySelector('p:nth-of-type(2)').textContent.toLowerCase();
    if (title.includes(searchInput) || description.includes(searchInput) || excerpt.includes(searchInput)) {
      post.style.display = 'block';
    } else {
      post.style.display = 'none';
    }
  });
}
</script>
