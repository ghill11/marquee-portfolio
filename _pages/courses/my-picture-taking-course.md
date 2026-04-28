---
title: "My picture taking course"
permalink: /courses/my-picture-taking-course/
layout: single
author_profile: true
classes: wide
description: "Approved portfolio artifacts produced for My picture taking course."
course_filter: "My picture taking course"
---

Approved portfolio artifacts produced for **{{ page.course_filter }}**.

{% assign filtered = site.artifacts | where: "course_label", page.course_filter | sort: "date" | reverse %}

{% if filtered.size == 0 %}

_No published artifacts for this course yet._

{% else %}

<div class="grid__wrapper">
{% for art in filtered %}
  <div class="grid__item">
    <article class="archive__item">
      {% if art.header.teaser %}
      <a href="{{ art.url | relative_url }}">
        <img src="{{ art.header.teaser | relative_url }}" alt="" class="archive__item-teaser">
      </a>
      {% endif %}
      <h2 class="archive__item-title"><a href="{{ art.url | relative_url }}">{{ art.title }}</a></h2>
      {% if art.is_featured %}<p><span class="badge--featured" title="Featured by Faculty">&#9733; Featured</span></p>{% endif %}
      {% if art.excerpt %}<p class="archive__item-excerpt">{{ art.excerpt | strip_html | truncate: 180 }}</p>{% endif %}
      {% if art.endorsement_quote and art.endorsement_quote != "" %}
      <blockquote class="endorsement endorsement--card">
        <p>&ldquo;{{ art.endorsement_quote | truncate: 140 }}&rdquo;</p>
        {% if art.endorser_name and art.endorser_name != "" %}<footer>&mdash; {{ art.endorser_name }}</footer>{% endif %}
      </blockquote>
      {% endif %}
    </article>
  </div>
{% endfor %}
</div>

{% endif %}

<p style="margin-top:1.5em"><a href="{{ '/courses/' | relative_url }}">&larr; All courses</a></p>
