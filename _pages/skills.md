---
title: "Skills"
permalink: /skills/
layout: single
author_profile: true
classes: wide
description: "Confirmed skills demonstrated across this Marquee portfolio, with evidence linked to the artifacts that demonstrate them."
---

{% assign all_tags_raw = "" | split: "" %}
{% for art in site.artifacts %}
  {% for t in art.tags %}
    {% assign all_tags_raw = all_tags_raw | push: t %}
  {% endfor %}
{% endfor %}
{% assign all_tags = all_tags_raw | uniq | sort %}

{% if all_tags.size == 0 %}

_No skills tagged on published artifacts yet._ As work is approved and published, this page will fill in automatically.

{% else %}

This page aggregates every confirmed skill across {{ site.artifacts | size }} published artifact{% if site.artifacts.size != 1 %}s{% endif %}. Each tag links to the artifacts that demonstrate it.

<div class="skills-grid">
{% for tag in all_tags %}
  {% assign evidence = site.artifacts | where_exp: "art", "art.tags contains tag" %}
  <section class="skill-block" id="skill-{{ tag | slugify }}">
    <h2 class="skill-block__title">
      <span class="skill-block__name">{{ tag }}</span>
      <span class="skill-block__count">{{ evidence.size }} artifact{% if evidence.size != 1 %}s{% endif %}</span>
    </h2>
    <ul class="skill-block__evidence">
    {% for art in evidence %}
      <li>
        <a href="{{ art.url | relative_url }}">{{ art.title }}</a>
        {% if art.is_featured %}<span class="badge--featured" title="Featured by Faculty">&#9733; Featured</span>{% endif %}
        {% if art.course_label %}<span class="skill-block__course">&middot; {{ art.course_label }}</span>{% endif %}
      </li>
    {% endfor %}
    </ul>
  </section>
{% endfor %}
</div>

{% endif %}
