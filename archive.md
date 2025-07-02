---
layout: page
title: Archive
---

# Monthly Progress

<!-- All posts organized by month. -->

{% assign posts_by_month = site.posts | group_by_exp: "post", "post.date | date: '%B %Y'" | sort: "name" | reverse %}

{% for month in posts_by_month %}
  <div class="month-group" style="margin-bottom: 2rem; padding: 1rem; border-left: 3px solid #e1e4e8; background: #f6f8fa; border-radius: 0 6px 6px 0;">
    <h2 style="margin: 0 0 1rem 0; color: #24292e; font-size: 1.5rem; font-weight: 600;">
      {{ month.name }}
    </h2>
    <ul style="list-style: none; padding: 0; margin: 0;">
      {% for post in month.items %}
        <li style="margin-bottom: 0.75rem; padding: 0.5rem 0; border-bottom: 1px solid #e1e4e8;">
          <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;">
            <a href="{{ site.baseurl }}{{ post.url }}" 
               style="text-decoration: none; color: #0366d6; font-weight: 500; flex: 1; margin-right: 1rem;"
               onmouseover="this.style.color='#0056b3'" 
               onmouseout="this.style.color='#0366d6'">
              {{ post.date | date: "%B %d" }}
            </a>
            <!-- <span style="color: #586069; font-size: 0.875rem; white-space: nowrap;">
              date: {{ post.date | date: "%Y-%m-%d" }} time started: {{ post.time_started | default: "N/A" }} time ended: {{ post.time_ended | default: "N/A" }}
            </span> -->
          </div>
          {% if post.excerpt %}
            <p style="margin: 0.5rem 0 0 0; color: #586069; font-size: 0.875rem; line-height: 1.4;">
              {{ post.excerpt | strip_html | truncatewords: 20 }}
            </p>
          {% endif %}
        </li>
      {% endfor %}
    </ul>
  </div>
{% endfor %}

<!-- <div style="text-align: center; margin-top: 3rem; padding: 2rem; background: #f6f8fa; border-radius: 8px;">
  <p style="margin: 0; color: #586069; font-size: 0.875rem;">
    📚 <strong>{{ site.posts.size }}</strong> posts and counting...
  </p>
  <p style="margin: 0.5rem 0 0 0; color: #586069; font-size: 0.875rem;">
    Follow the journey from Day 0 to building the future of AI-powered solutions.
  </p>
</div> -->