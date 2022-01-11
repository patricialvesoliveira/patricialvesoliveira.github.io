---
layout: default
title: Tags
permalink: /tags/
exclude: true
---

<ul class="blog-tags-list">

  {% assign sorted_tags = site.categories | sort %}
  {% for tag in sorted_tags %}
    {% assign t = tag | first %}
    {% assign posts = tag | last %}
    {% assign numPosts = posts | size %}
    <li class="blog-tag-item" id="{{ t | downcase | remove: ' ' }}-item">
      <a href onclick="filter('{{ t }}'); return false;">{{ t | replace: '-', ' '}}
	    {% if numPosts == 1 %}
	      <span>({{ posts | size }} post)</span>
	    {% else %}
	      <span>({{ posts | size }} posts)</span>
	    {% endif %}
      </a>
    </li>
  {% endfor %}
</ul>

{% for tag in site.categories %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}
  <div class="blog-list-container hidden" id="{{ t | downcase | remove: ' ' }}-container">
    <ul class="blog-list">
    	<b>{{ t | replace: '-', ' '}}</b>
      {% for post in posts %}
        {% if post.categories contains t %}
          <li>
            <span class="blog-item-date">{{ post.date | date: "%d %b %Y" }}</span>
            <a href="{{ post.url }}">{{ post.title }}</a>
          </li>
        {% endif %}
      {% endfor %}
    </ul>

  </div>
{% endfor %}

<script>
if(window.location.hash) {
  var tag = window.location.hash.split('#')[1];
  filter(tag);
}
</script>