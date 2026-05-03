---
layout: a_new_page
title: 'Idea'
permalink: /idea/
---

<style>
.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(450px, 1fr));
  gap: 0;
  max-width: 1000px;
  margin: 0 auto;
}

.blog-item {
  display: flex;
  gap: 16px;
  padding: 24px 16px;
  border-bottom: 1px solid #eaeaea;
  text-decoration: none;
  color: inherit;
  transition: background 0.2s;
}

.blog-item:hover {
  background: #f6f8fa;
}

.blog-item:hover .blog-title {
  color: #0969da;
  text-decoration: underline;
}

.blog-thumbnail {
  flex-shrink: 0;
  width: 120px;
  height: 80px;
  border-radius: 8px;
  background: #d9d2e9;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.blog-thumbnail-icon {
  font-size: 1.6rem;
  opacity: 0.6;
}

.blog-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.blog-category a {
  font-size: 0.72rem;
  font-weight: 700;
  color: #6639ba !important;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.blog-title {
  font-size: 1rem;
  font-weight: 700;
  color: #1a1a2e;
  line-height: 1.4;
  margin: 0;
}

.blog-excerpt {
  font-size: 0.85rem;
  color: #555;
  line-height: 1.5;
  margin: 0;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.blog-meta {
  font-size: 0.78rem;
  color: #888;
  margin-top: auto;
}

.blog-meta strong {
  color: #444;
}

@media (max-width: 600px) {
  .blog-grid {
    grid-template-columns: 1fr;
  }
  .blog-thumbnail {
    width: 90px;
    height: 65px;
  }
}
</style>

<div class="blog-grid">
  {% assign sharepoint_posts = site.posts | where: "lang", "en" %}
  {% for post in sharepoint_posts %}
    {% if post.tags contains "idea" %}
    <div class="blog-item">
      <div class="blog-thumbnail">
        <span class="blog-thumbnail-icon" style="font-size:1.6rem; opacity:0.9;">🔮</span>
      </div>
      <div class="blog-content">
        <h3 class="blog-title"><a href="{{ post.url }}">{{ post.judul }}</a></h3>
        <p class="blog-excerpt">{{ post.description }}</p>
        <span class="blog-meta">
          {{ post.date | date: "%d %B %Y" }}
        </span>
      </div>
    </div>
    {% endif %}
  {% endfor %}
</div>
