---
layout: page
title: Archive
---

# Weekly Progress & Time Tracking

<!-- All posts organized by week with hours worked calculation. -->

{% assign posts_by_week = site.posts | group_by_exp: "post", "post.date | date: '%Y-W%U'" | sort: "name" | reverse %}

---

<!-- All posts organized by week with hardcoded hours worked. -->

{% assign posts_by_week = site.posts | group_by_exp: "post", "post.date | date: '%Y-W%U'" | sort: "name" | reverse %}

{% for week in posts_by_week %}
  {% assign week_name = "" %}
  {% assign week_hours = 0 %}
  {% for post in week.items %}
    {% if forloop.first %}
      {% assign week_name = post.date | date: "Week of %B %d, %Y" %}
      {% assign week_start_date = post.date | date: "%Y-%m-%d" %}
      {% if week_start_date >= "2025-06-24" and week_start_date <= "2025-06-27" %}
        {% assign week_hours = 28.2 %}
      {% elsif week_start_date >= "2025-06-30" and week_start_date <= "2025-07-02" %}
        {% assign week_hours = 20.5 %}
      {% endif %}
    {% endif %}
  {% endfor %}
  
  <div class="week-group" style="margin-bottom: 2rem; padding: 1rem; border-left: 3px solid #28a745; background: #f8f9fa; border-radius: 0 6px 6px 0;">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; flex-wrap: wrap;">
      <h2 style="margin: 0; color: #24292e; font-size: 1.5rem; font-weight: 600;">
        {{ week_name }}
      </h2>
      <div style="background: #28a745; color: white; padding: 0.25rem 0.75rem; border-radius: 12px; font-size: 0.875rem; font-weight: 500; margin-left: 1rem;">
        {{ week_hours }}h worked
      </div>
    </div>
    <ul style="list-style: none; padding: 0; margin: 0;">
      {% for post in week.items %}
        <li style="margin-bottom: 0.75rem; padding: 0.5rem 0; border-bottom: 1px solid #e1e4e8;">
          <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;">
            <a href="{{ site.baseurl }}{{ post.url }}" 
               style="text-decoration: none; color: #0366d6; font-weight: 500; flex: 1; margin-right: 1rem;"
               onmouseover="this.style.color='#0056b3'" 
               onmouseout="this.style.color='#0366d6'">
              {{ post.date | date: "%B %d" }}
            </a>
            {% assign time_started = post["time started"] %}
            {% assign time_ended = post["time ended"] %}
            {% if time_started and time_ended %}
              <span style="color: #6f42c1; font-size: 0.75rem; white-space: nowrap; background: #f8f9fa; padding: 0.125rem 0.5rem; border-radius: 8px; border: 1px solid #e1e4e8;">
                {{ time_started }} - {{ time_ended }}
              </span>
            {% endif %}
          </div>
          {% if post.summary %}
            <p style="margin: 0.5rem 0 0 0; color: #586069; font-size: 0.875rem; line-height: 1.4;">
              {{ post.summary }}
            </p>
          {% elsif post.excerpt %}
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