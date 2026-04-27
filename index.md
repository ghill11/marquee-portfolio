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
excerpt: "3 published artifacts."
intro:
  - excerpt: "Selected academic and professional work from the University of Central Arkansas, published through Marquee. Browse below or filter by skill from any artifact page."
---

{% include feature_row id="intro" type="center" %}

{% assign flagship = site.artifacts | where: "is_flagship", true | first %}
{% if flagship %}
## Flagship project

<section class="flagship">
  {% if flagship.header.teaser %}
  <a class="flagship__teaser" href="{{ flagship.url | relative_url }}">
    <img src="{{ flagship.header.teaser | relative_url }}" alt="">
  </a>
  {% endif %}
  <div class="flagship__body">
    <h2 class="flagship__title"><a href="{{ flagship.url | relative_url }}">{{ flagship.title }}</a></h2>
    {% if flagship.course_label %}<p class="flagship__course"><em>{{ flagship.course_label }}</em></p>{% endif %}
    {% if flagship.is_featured %}<p><span class="badge--featured" title="Featured by Faculty">&#9733; Featured</span></p>{% endif %}
    {% if flagship.excerpt %}<p class="flagship__excerpt">{{ flagship.excerpt | strip_html | truncate: 280 }}</p>{% endif %}
    {% if flagship.endorsement_quote and flagship.endorsement_quote != "" %}
    <blockquote class="endorsement endorsement--card">
      <p>&ldquo;{{ flagship.endorsement_quote | truncate: 200 }}&rdquo;</p>
      {% if flagship.endorser_name and flagship.endorser_name != "" %}<footer>&mdash; {{ flagship.endorser_name }}</footer>{% endif %}
    </blockquote>
    {% endif %}
  </div>
</section>
{% endif %}

## Published artifacts

{% assign sorted = site.artifacts | sort: 'date' | reverse %}
{% if sorted.size == 0 %}
_No artifacts published yet._
{% else %}
<div class="grid__wrapper">
{% for art in sorted %}
  {% if art.is_flagship %}{% continue %}{% endif %}
  <div class="grid__item">
    <article class="archive__item">
      {% if art.header.teaser %}
      <a href="{{ art.url | relative_url }}">
        <img src="{{ art.header.teaser | relative_url }}" alt="" class="archive__item-teaser">
      </a>
      {% endif %}
      <h2 class="archive__item-title"><a href="{{ art.url | relative_url }}">{{ art.title }}</a></h2>
      {% if art.is_featured %}<p><span class="badge--featured" title="Featured by Faculty">&#9733; Featured</span></p>{% endif %}
      {% if art.course_label %}<p class="archive__item-excerpt"><em>{{ art.course_label }}</em></p>{% endif %}
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
