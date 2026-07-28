---
layout: home
title: Latest Articles
---

Welcome to my space! I write about hydrology research, climate systems, coding, and navigating life here in Japan.

## Filter by Topic

<!-- Styled Tag Buttons -->
<div style="margin-bottom: 25px; display: flex; flex-wrap: wrap; gap: 8px;">
  <button onclick="filterTag('all', this)" class="tag-btn active-tag" style="padding: 6px 14px; border: 1px solid #007681; background-color: #007681; color: white; border-radius: 20px; font-size: 14px; cursor: pointer; transition: all 0.2s ease; font-weight: 500;">All Posts</button>
  {% assign tags = site.tags | sort %}
  {% for tag in tags %}
    <button onclick="filterTag('{{ tag }}', this)" class="tag-btn" style="padding: 6px 14px; border: 1px solid #d1d5db; background-color: #f9fafb; color: #374151; border-radius: 20px; font-size: 14px; cursor: pointer; transition: all 0.2s ease; font-weight: 500;">#{{ tag }}</button>
  {% endfor %}
</div>

## Recent Posts

<!-- Post List -->
<ul id="post-list" style="list-style: none; padding-left: 0;">
  {% for post in site.posts %}
    <li class="post-item" data-tags="{{ post.tags | join: ',' }}" style="margin-bottom: 20px; border-bottom: 1px solid #f3f4f6; padding-bottom: 15px;">
      <span style="color: #6b7280; font-size: 14px; display: block; margin-bottom: 4px;">{{ post.date | date: "%B %d, %Y" }}</span>
      <a href="{{ post.url | relative_url }}" style="font-size: 18px; font-weight: 600; color: #1f2937; text-decoration: none; transition: color 0.2s;">{{ post.title }}</a>
      <div style="margin-top: 6px; display: flex; gap: 6px;">
        {% for post_tag in post.tags %}
          <span style="font-size: 12px; background-color: #f3f4f6; color: #4b5563; padding: 2px 8px; border-radius: 4px;">#{{ post_tag }}</span>
        {% endfor %}
      </div>
    </li>
  {% endfor %}
</ul>

<!-- JavaScript Filter & Style Logic -->
<script>
function filterTag(tagName, clickedButton) {
  // 1. Reset all button styles to default unselected look
  const buttons = document.querySelectorAll('.tag-btn');
  buttons.forEach(btn => {
    btn.style.backgroundColor = '#f9fafb';
    btn.style.color = '#374151';
    btn.style.borderColor = '#d1d5db';
  });

  // 2. Apply active highlighted style to the clicked button
  clickedButton.style.backgroundColor = '#007681';
  clickedButton.style.color = 'white';
  clickedButton.style.borderColor = '#007681';

  // 3. Filter the posts list instantly
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

// Subtle hover effects for buttons via JS since inline hover CSS is limited
document.querySelectorAll('.tag-btn').forEach(btn => {
  btn.addEventListener('mouseenter', () => {
    if (btn.style.backgroundColor !== 'rgb(0, 118, 129)') { // If not selected
      btn.style.backgroundColor = '#e5e7eb';
    }
  });
  btn.addEventListener('mouseleave', () => {
    if (btn.style.backgroundColor !== 'rgb(0, 118, 129)') { // If not selected
      btn.style.backgroundColor = '#f9fafb';
    }
  });
});
</script>
