---
title: "Courses"
permalink: /courses/
layout: single
author_profile: true
classes: wide
description: "Portfolio artifacts grouped by the course that produced them. Each course links to a dedicated page listing every approved artifact for that course."
---

{% assign labels_raw = site.artifacts | map: "course_label" | compact | uniq | sort %}

{% if labels_raw.size == 0 %}

_No courses tagged on published artifacts yet._ As work is approved and published with a course label, this page will fill in automatically.

{% else %}

This portfolio's published work is grouped by course. Each course page lists every approved artifact for that course.

<ul class="course-index">
{% for label in labels_raw %}
  {% assign in_course = site.artifacts | where: "course_label", label %}
  <li>
    <a href="{{ '/courses/' | append: label | slugify | append: '/' | relative_url }}">
      <strong>{{ label }}</strong>
    </a>
    <span class="course-index__count">{{ in_course.size }} artifact{% if in_course.size != 1 %}s{% endif %}</span>
  </li>
{% endfor %}
</ul>

{% endif %}
