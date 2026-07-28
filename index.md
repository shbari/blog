---
layout: home
title: Latest Articles
---

<!-- Core CSS Styles for Full Responsiveness & Theme UI -->
<style>
  .blog-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 10px;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  }
  .intro-text {
    font-size: 1.15rem;
    line-height: 1.6;
    color: #4b5563;
    margin-bottom: 30px;
  }
  .section-title {
    font-size: 1.4rem;
    font-weight: 700;
    color: #111827;
    border-bottom: 2px solid #e5e7eb;
    padding-bottom: 8px;
    margin-bottom: 20px;
    margin-top: 30px;
  }
  
  /* Modern Search Bar Styles */
  .search-wrapper {
    position: relative;
    margin-bottom: 20px;
  }
  .search-input {
    width: 100%;
    padding: 12px 16px;
    font-size: 1rem;
    border: 1px solid #d1d5db;
    border-radius: 8px;
    background-color: #ffffff;
    color: #111827;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
    outline: none;
    transition: all 0.2s ease;
    box-sizing: border-box;
  }
  .search-input:focus {
    border-color: #007681;
    box-shadow: 0 0 0 3px rgba(0, 118, 129, 0.15);
  }

  /* Tag Filtering Styles */
  .tag-container {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 20px;
  }
  .tag-btn {
    padding: 8px 16px;
    border: 1px solid #e5e7eb;
    background-color: #f9fafb;
    color: #4b5563;
    border-radius: 30px;
    font-size: 0.9rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.25s ease;
    box-shadow: 0 1px 2px rgba(0,0,0,0.05);
    -webkit-tap-highlight-color: transparent;
  }
  
  /* Article Post Feed List Layout */
  .post-list {
    list-style: none;
    padding-left: 0;
    margin: 0;
  }
  .post-item {
    padding: 20px 0;
    border-bottom: 1px solid #f3f4f6;
    transition: transform 0.2s ease;
  }
  @media (min-width: 768px) {
    .post-item:hover {
      transform: translateX(4px);
    }
  }
  .post-date {
    color: #9ca3af;
    font-size: 0.85rem;
    font-weight: 500;
    display: block;
    margin-bottom: 6px;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
  .post-link {
    font-size: 1.3rem;
    font-weight: 700;
    color: #111827;
    text-decoration: none;
    line-height: 1.4;
    display: inline-block;
    transition: color 0.2s ease;
  }
  .post-link:hover {
    color: #007681;
  }
  .item-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-top: 10px;
  }
  .inline-tag {
    font-size: 0.75rem;
    background-color: #f3f4f6;
    color: #6b7280;
    padding: 3px 10px;
    border-radius: 12px;
    font-weight: 500;
  }
  .no-results {
    display: none;
    padding: 30px 0;
    color: #6b7280;
    font-style: italic;
    text-align: center;
  }
</style>

<div class="blog-container">
  <p class="intro-text">
    Welcome to my space! I write casually about hydrology research, climate change impacts, coding, and navigating life here in Japan.
  </p>

  <h2 class="section-title">Search & Filter</h2>

  <!-- Integrated Real-time Search Input -->
  <div class="search-wrapper">
    <input type="text" id="search-bar" class="search-input" placeholder="Search by article title or keywords..." onkeyup="executeSearchAndFilter()">
  </div>

  <!-- Responsive Dynamic Tag Menu -->
  <div class="tag-container">
    <button onclick="selectTag('all', this)" class="tag-btn" id="default-tag-btn" style="background-color: #007681; color: white; border-color: #007681;">All Posts</button>
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
      <button onclick="selectTag('{{ tag }}', this)" class="tag-btn">#{{ tag }}</button>
    {% endfor %}
  </div>

  <h2 class="section-title">Recent Posts</h2>

  <!-- Post Items Card List -->
  <ul id="post-list" class="post-list">
    {% for post in site.posts %}
      <li class="post-item" data-title="{{ post.title | downcase }}" data-tags="{{ post.tags | join: ',' | downcase }}">
        <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
        <a href="{{ post.url | relative_url }}" class="post-link">{{ post.title }}</a>
        <div class="item-tags">
          {% for post_tag in post.tags %}
            <span class="inline-tag">#{{ post_tag }}</span>
          {% endfor %}
        </div>
      </li>
    {% endfor %}
  </ul>

  <!-- Fallback message when no matches are found -->
  <div id="no-results-msg" class="no-results">
    No articles found matching your criteria. Try another keyword!
  </div>
</div>

<!-- Combined High-Performance Searching & Filtering Logic -->
<script>
let currentActiveTag = 'all';

function selectTag(tagName, clickedButton) {
  // 1. Reset all button styles to default unselected look
  const buttons = document.querySelectorAll('.tag-btn');
  buttons.forEach(btn => {
    btn.style.backgroundColor = '#f9fafb';
    btn.style.color = '#4b5563';
    btn.style.borderColor = '#e5e7eb';
  });

  // 2. Highlight selected button and update track state
  clickedButton.style.backgroundColor = '#007681';
  clickedButton.style.color = 'white';
  clickedButton.style.borderColor = '#007681';
  currentActiveTag = tagName.toLowerCase();

  // 3. Process the changes instantly
  executeSearchAndFilter();
}

function executeSearchAndFilter() {
  const searchQueries = document.getElementById('search-bar').value.toLowerCase().trim();
  const posts = document.querySelectorAll('.post-item');
  let visibleCount = 0;

  posts.forEach(post => {
    const postTitle = post.getAttribute('data-title');
    const postTags = post.getAttribute('data-tags').split(',');

    // Evaluate tag criteria
    const matchesTag = (currentActiveTag === 'all' || postTags.includes(currentActiveTag));
    
    // Evaluate search bar criteria
    const matchesSearch = (postTitle.includes(searchQueries) || postTags.some(t => t.includes(searchQueries)));

    // Combined conditional visibility check
    if (matchesTag && matchesSearch) {
      post.style.display = 'block';
      visibleCount++;
    } else {
      post.style.display = 'none';
    }
  });

  // Toggle "No results" banner dynamically
  const fallbackMsg = document.getElementById('no-results-msg');
  if (visibleCount === 0) {
    fallbackMsg.style.display = 'block';
  } else {
    fallbackMsg.style.display = 'none';
  }
}

// Mobile/Tablet-friendly hover handling via event listeners
document.querySelectorAll('.tag-btn').forEach(btn => {
  btn.addEventListener('mouseenter', () => {
    if (btn.style.backgroundColor !== 'rgb(0, 118, 129)') {
      btn.style.backgroundColor = '#e5e7eb';
      btn.style.color = '#111827';
    }
  });
  btn.addEventListener('mouseleave', () => {
    if (btn.style.backgroundColor !== 'rgb(0, 118, 129)') {
      btn.style.backgroundColor = '#f9fafb';
      btn.style.color = '#4b5563';
    }
  });
});
</script>
