---
# Custom Marquee landing layout (defined in
# _layouts/marquee_landing.html). Replaces MM's `single` so we don't
# fight the reserved sidebar slot, the $max-width cap on #main, or the
# standalone .page__title h2. The browser tab title and jekyll-seo-tag
# both fall back to site.title (set by _config.yml.tmpl).
layout: marquee_landing
permalink: /
header:
  og_image: /assets/covers/_landing.png
---

<div class="marquee-landing-shell">
  <section class="marquee-landing-shell__hero">
    <section class="marquee-landing-hero" aria-label="Portfolio overview">
  <div class="marquee-landing-hero__body">
    <p class="marquee-landing-hero__tagline">3 published artifacts.</p>
    <p class="marquee-landing-hero__intro">Selected academic and professional work from the University of Central Arkansas, published through Marquee. Browse below or filter by skill from any artifact page.</p>
    <ul class="marquee-landing-hero__stats">
      <li><strong>3</strong> artifacts</li>
      <li><strong>2</strong> courses</li>
      <li><strong>1</strong> skill</li>
      <li>Updated {{ site.marquee.generated_at | date: "%b %-d, %Y" }}</li>
    </ul>
    <div class="marquee-landing-hero__badges"><p class="marquee-badges"><img alt="2 courses represented" src="https://img.shields.io/badge/Courses-2-552583?style=flat"><img alt="1 skills demonstrated" src="https://img.shields.io/badge/Skills-1-552583?style=flat"><img alt="1 faculty-featured artifacts" src="https://img.shields.io/badge/Featured-1-eab308?style=flat"><img alt="Verified by UCA CISA" src="https://img.shields.io/badge/Verified_by-UCA_CISA-552583?style=flat"></p></div>
    <div class="marquee-landing-hero__actions">
      <a class="btn btn--primary" href="https://github.com/ghill11/marquee-portfolio">View on GitHub</a>
    </div>
  </div>
</section>

  </section>
  {% assign flagship = site.artifacts | where: "is_flagship", true | first %}
  {% if flagship %}
  <aside class="marquee-landing-shell__rail">
    <div class="flagship__pin-label"><span aria-hidden="true">&#9733;</span> Flagship project</div>
    <section class="flagship" data-tags="{{ flagship.tags | join: '|' }}">
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
    {% assign w = flagship.content | number_of_words %}
    {% assign rt = w | divided_by: 220 | plus: 1 %}
    <div class="card-meta">
      <span class="card-meta__chip" title="Estimated reading time">{{ rt }} min read</span>
      <span class="card-meta__chip" title="Skills demonstrated">{{ flagship.tags | size }} skill{% if flagship.tags.size != 1 %}s{% endif %}</span>
      <span class="card-meta__chip" title="Word count">{{ w }} words</span>
      <span class="card-meta__chip" title="Last updated">Updated {{ flagship.last_modified_at | date: "%b %-d, %Y" }}</span>
    </div>
    {% if flagship.endorsement_quote and flagship.endorsement_quote != "" %}
    <blockquote class="endorsement endorsement--card">
      <p>&ldquo;{{ flagship.endorsement_quote | truncate: 200 }}&rdquo;</p>
      {% if flagship.endorser_name and flagship.endorser_name != "" %}<footer>&mdash; {{ flagship.endorser_name }}</footer>{% endif %}
    </blockquote>
    {% endif %}
  </div>
    </section>
  </aside>
  {% endif %}
  <section class="marquee-landing-shell__below" markdown="1">

{% assign all_tags_raw = "" | split: "" %}
{% for art in site.artifacts %}{% for t in art.tags %}
  {% assign all_tags_raw = all_tags_raw | push: t %}
{% endfor %}{% endfor %}
{% assign all_tags = all_tags_raw | uniq | sort %}
{% if site.artifacts.size > 1 and all_tags.size > 0 %}
<div class="marquee-skill-filter" role="group" aria-label="Filter by skill">
  <span class="marquee-skill-filter__label">Filter by skill:</span>
  {% for tag in all_tags %}
  <a class="skill-pill" href="#" data-filter="{{ tag }}">{{ tag }}</a>
  {% endfor %}
  <a class="marquee-skill-filter__clear skill-pill" href="#" style="background:transparent;border-style:dashed;">Clear</a>
</div>
{% endif %}

## Published artifacts

{% assign sorted = site.artifacts | sort: 'date' | reverse %}
{% if sorted.size == 0 %}
_No artifacts published yet._
{% else %}
<div class="grid__wrapper">
{% for art in sorted %}
  {% if art.is_flagship %}{% continue %}{% endif %}
  <div class="grid__item" data-tags="{{ art.tags | join: '|' }}">
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
      {% assign w = art.content | number_of_words %}
      {% assign rt = w | divided_by: 220 | plus: 1 %}
      <div class="card-meta">
        <span class="card-meta__chip" title="Estimated reading time">{{ rt }} min read</span>
        <span class="card-meta__chip" title="Skills demonstrated">{{ art.tags | size }} skill{% if art.tags.size != 1 %}s{% endif %}</span>
        <span class="card-meta__chip" title="Word count">{{ w }} words</span>
        <span class="card-meta__chip" title="Last updated">Updated {{ art.last_modified_at | date: "%b %-d, %Y" }}</span>
      </div>
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
  </section>
</div>
