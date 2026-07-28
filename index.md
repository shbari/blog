---
layout: home
title: Latest Articles
---

Welcome to my space! I write about hydrology research, climate systems, coding, and navigating life here in Japan.

## Filter by Topic
<!-- Tag Buttons -->
<div style="margin-bottom: 20px;">
  <button onclick="filterTag('all')" class="tag-btn" style="padding: 5px 10px; margin-right: 5px; cursor: pointer;">All Posts</button>
  {% assign tags = site.tags | sort %}
  {% for tag in tags %}
    <button onclick="filterTag('{{ tag[0] }}')" class="tag-btn" style="padding: 5px 10px; margin-right: 5px; cursor: pointer;">#{{ tag[0] }}</button>
  {% endfor %}
</div>

## Recent Posts
<!-- Post List -->
<ul id="post-list" style="list-style: none; padding-left: 0;">
  {% for post in site.posts %}
    <li class="post-item" data-tags="{{ post.tags | join: ',' }}" style="margin-bottom: 15px;">
      <strong>{{ post.date | date: "%B %d, %Y" }}</strong> — 
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <br>
      <small style="color: gray;">Tags: {{ post.tags | join: ', ' }}</small>
    </li>
  {% endfor %}
</ul>

<!-- JavaScript Filter Logic -->
<script>
function filterTag(tagName) {
  const posts = document.querySelectorAll('.post-item');
  
  posts.forEach(post => {
    if (tagName === 'all') {
      post.style.display = 'block';
    } else {
      const postTags = post.getAttribute('data-tags').split(',');
      if (postTags.includes(tagName)) {
        post.style.display = 'block';
      } else {
        post.style.display = 'none';
      }
    }
  });
}
</script>
