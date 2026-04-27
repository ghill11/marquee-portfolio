---
title: "Dr. Geoffrey Hill"
layout: splash
permalink: /
header:
  # Landing cover is pure visual chrome (no name baked in); MM overlays
  # the page title (the student's name) as live text on top.
  overlay_color:  "#552583"
  overlay_image:  /assets/covers/_landing.png
  overlay_filter: "0.35"
  og_image:       /assets/covers/_landing.png
  caption: "Marquee Portfolio at the University of Central Arkansas"
  actions:
    - label: "View on GitHub"
      url:   "https://github.com/ghill11/marquee-portfolio"
excerpt: "Portfolio coming soon."
intro:
  - excerpt: "This portfolio is published via Marquee at the University of Central Arkansas. New work will appear here as it is approved."
---

{% include feature_row id="intro" type="center" %}

## Published artifacts

{% assign sorted = site.artifacts | sort: 'date' | reverse %}
{% if sorted.size == 0 %}
_No artifacts published yet._
{% else %}
<div class="grid__wrapper">
{% for art in sorted %}
  <div class="grid__item">
    <article class="archive__item">
      {% if art.header.teaser %}
      <a href="{{ art.url | relative_url }}">
        <img src="{{ art.header.teaser | relative_url }}" alt="" class="archive__item-teaser">
      </a>
      {% endif %}
      <h2 class="archive__item-title"><a href="{{ art.url | relative_url }}">{{ art.title }}</a></h2>
      {% if art.course_label %}<p class="archive__item-excerpt"><em>{{ art.course_label }}</em></p>{% endif %}
      {% if art.excerpt %}<p class="archive__item-excerpt">{{ art.excerpt | strip_html | truncate: 180 }}</p>{% endif %}
    </article>
  </div>
{% endfor %}
</div>
{% endif %}
