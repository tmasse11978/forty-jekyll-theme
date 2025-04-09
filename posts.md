---
layout: post
title: Blog
pagination:
  enabled: true
  collection: blog
---

<section id="two" class="spotlights">
{% for post in paginator.posts %}
    {% if post.title != 404 %}
        <section class="post-tile{% if forloop.last %} mb-2{% endif %}">
            {% if post.image %}
                <a href="{{ site.baseurl }}/{{ post.url }}/" class="image">
                    <img src="{{ site.baseurl }}/{{ post.image }}" alt="{{ post.title }}" data-position="center center" />
                </span>
            {% endif %}
            <div class="content">
                <div class="inner">
                    <header class="major">
                        <h3>{{ post.title }}</h3>
                        <em class="date">
                            {% if post.date %}
                            {{ post.date | date: "%-d %B %Y" }}
                            {% endif %}
                        </em>
                    </header>
                    <p>{{ post.description }}</p>
                    <ul class="actions">
                        <li><a href="{{ site.baseurl }}/{{ post.url }}/" class="button">Learn more</a></li>
                    </ul>
                </div>
            </div>
        </section>
    {% endif %}
{% endfor %}
</section>
<!-- 
    Showing buttons to move to the next and to the previous list of posts (pager buttons).
  -->
  {% if paginator.total_pages > 1 %}
  <ul class="pager">
      {% if paginator.first_page %}
      <li class="previous">
          <a href="{{ paginator.first_page_path | prepend: site.baseurl | replace: '//', '/' }}">First</a>
      </li>
      {% endif %}

      {% if paginator.previous_page %}
      <li class="previous">
          <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Newer Posts</a>
      </li>
      {% endif %}

        {% if paginator.page_trail %}
            {% assign current = page.url | replace:'index.html','' | replace:'//','/' %}
            {% for trail in paginator.page_trail %}
                {% assign trail_path = trail.path | replace:'index.html','' | replace:'//','/' %}
                <li class="{% if current == trail_path %}selected{% endif %}">
                {% if current == trail_path %}
                    <span>{{ trail.num }}</span>
                {% else %}
                    <a href="{{ trail.path | prepend: site.baseurl | replace: '//','/' }}" title="{{ trail.title }}">{{ trail.num }}</a>
                {% endif %}
                </li>
            {% endfor %}
        {% endif %}

      {% if paginator.next_page %}
      <li class="next">
          <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Older Posts &rarr;</a>
      </li>
      {% endif %}

       {% if paginator.last_page %}
      <li class="previous">
          <a href="{{ paginator.last_page_path | prepend: site.baseurl | replace: '//', '/' }}">Last</a>
      </li>
      {% endif %}
  </ul>
  {% endif %}