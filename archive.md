---
layout: page
title: Archive
---

# Weekly Progress & Time Tracking

<!-- All posts organized by week with hours worked calculation. -->

{% assign posts_by_week = site.posts | group_by_exp: "post", "post.date | date: '%Y-W%U'" | sort: "name" | reverse %}

{% for week in posts_by_week %}
  {% assign week_hours = 0 %}
  {% assign week_name = "" %}
  {% for post in week.items %}
    {% assign time_started = post["time started"] %}
    {% assign time_ended = post["time ended"] %}
    {% if time_started and time_ended %}
      {% assign start_parts = time_started | split: ":" %}
      {% assign end_parts = time_ended | split: ":" %}
      {% assign start_hour = start_parts[0] | plus: 0 %}
      {% assign start_min_part = start_parts[1] | split: " " %}
      {% assign start_min = start_min_part[0] | plus: 0 %}
      {% assign start_ampm = start_min_part[1] %}
      
      {% assign end_hour = end_parts[0] | plus: 0 %}
      {% assign end_min_part = end_parts[1] | split: " " %}
      {% assign end_min = end_min_part[0] | plus: 0 %}
      {% assign end_ampm = end_min_part[1] %}
      
      <!-- Convert to 24-hour format -->
      {% if start_ampm == "PM" and start_hour != 12 %}
        {% assign start_hour = start_hour | plus: 12 %}
      {% elsif start_ampm == "AM" and start_hour == 12 %}
        {% assign start_hour = 0 %}
      {% endif %}
      
      {% if end_ampm == "PM" and end_hour != 12 %}
        {% assign end_hour = end_hour | plus: 12 %}
      {% elsif end_ampm == "AM" and end_hour == 12 %}
        {% assign end_hour = 0 %}
      {% endif %}
      
      {% assign start_total_min = start_hour | times: 60 | plus: start_min %}
      {% assign end_total_min = end_hour | times: 60 | plus: end_min %}
      {% assign duration_min = end_total_min | minus: start_total_min %}
      
      <!-- Handle overnight sessions -->
      {% if duration_min < 0 %}
        {% assign duration_min = duration_min | plus: 1440 %}
      {% endif %}
      
      {% assign duration_hours = duration_min | divided_by: 60.0 %}
      {% assign week_hours = week_hours | plus: duration_hours %}
    {% endif %}
    {% if forloop.first %}
      {% assign week_name = post.date | date: "Week of %B %d, %Y" %}
    {% endif %}
  {% endfor %}
  
  <div class="week-group" style="margin-bottom: 2rem; padding: 1rem; border-left: 3px solid #28a745; background: #f8f9fa; border-radius: 0 6px 6px 0;">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; flex-wrap: wrap;">
      <h2 style="margin: 0; color: #24292e; font-size: 1.5rem; font-weight: 600;">
        {{ week_name }}
      </h2>
      <div style="background: #28a745; color: white; padding: 0.25rem 0.75rem; border-radius: 12px; font-size: 0.875rem; font-weight: 500; margin-left: 1rem;">
        {{ week_hours | round: 1 }}h worked
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