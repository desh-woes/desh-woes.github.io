---
layout: page
title: Archive
---

<section class="archive-section">
  {% if site.posts[0] %}
    {% assign currentyear = 'now' | date: "%Y" %}
    {% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
    
    <div class="archive-header">
      <h1 class="archive-title">Archive</h1>
      <p class="archive-subtitle">All posts organized by year</p>
    </div>

    <div class="archive-content">
      {% for year_group in posts_by_year %}
        {% assign year = year_group.name %}
        {% assign year_posts = year_group.items %}
        <div class="archive-year-group">
          <div class="archive-year-header">
            <h2 class="archive-year-title">
              {% if year == currentyear %}
                This Year
              {% else %}
                {{ year }}
              {% endif %}
            </h2>
            <span class="archive-year-count">{{ year_posts.size }} {% if year_posts.size == 1 %}post{% else %}posts{% endif %}</span>
          </div>
          <ul class="archive-posts-list">
            {% for post in year_posts %}
              <li class="archive-post-item">
                <time class="archive-post-date" datetime="{{ post.date | date: '%Y-%m-%d' }}">
                  {{ post.date | date: "%b %d" }}
                </time>
                <a href="{{ post.url | prepend: site.baseurl | replace: '//', '/' }}" class="archive-post-link">
                  {{ post.title }}
                </a>
              </li>
            {% endfor %}
          </ul>
        </div>
      {% endfor %}
    </div>
  {% else %}
    <div class="archive-empty">
      <p>No posts yet. Check back soon!</p>
    </div>
  {% endif %}
</section>