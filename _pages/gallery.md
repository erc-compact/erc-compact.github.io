---
layout: page
title: Gallery
permalink: /gallery/
description: Photos from the COMPACT team — events, conferences, and beyond.
nav: true
nav_rank: 7
---

{%- assign photos = site.data.gallery -%}
{%- assign categories = photos | map: "category" | uniq | sort -%}

<div class="gallery-filter">
  <button class="gallery-btn active" data-filter="all">All</button>
  {%- for cat in categories %}
  <button class="gallery-btn" data-filter="{{ cat }}">{{ cat | capitalize }}</button>
  {%- endfor %}
</div>

<div class="gallery-grid" id="gallery-grid">
  {%- for photo in photos %}
  {%- assign src_path = photo.file | prepend: "/" | prepend: photo.category | prepend: "assets/img/gallery/" %}
  {%- assign alt_text = photo.alt | default: photo.caption | default: photo.file %}
  <div class="gallery-card" data-category="{{ photo.category }}">
    <img
      src="{{ src_path | relative_url }}"
      alt="{{ alt_text }}"
      class="gallery-img"
      data-zoomable
      loading="lazy"
    >
    {%- if photo.caption %}
    <div class="gallery-caption">{{ photo.caption }}</div>
    {%- endif %}
  </div>
  {%- endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  var buttons = document.querySelectorAll('.gallery-btn');
  var cards   = document.querySelectorAll('.gallery-card');

  buttons.forEach(function (btn) {
    btn.addEventListener('click', function () {
      buttons.forEach(function (b) { b.classList.remove('active'); });
      btn.classList.add('active');
      var filter = btn.getAttribute('data-filter');
      cards.forEach(function (card) {
        card.style.display =
          (filter === 'all' || card.getAttribute('data-category') === filter)
          ? '' : 'none';
      });
      if (typeof $ !== 'undefined' && $('.grid').data('masonry')) {
        $('.grid').masonry('layout');
      }
    });
  });
});
</script>

<style>
/* ── Filter bar ─────────────────────────────────────────── */
.gallery-filter {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 2rem;
}

.gallery-btn {
  padding: 0.35rem 1.1rem;
  border-radius: 999px;
  border: 1.5px solid var(--global-theme-color);
  background: transparent;
  color: var(--global-theme-color);
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  cursor: pointer;
  transition: background 0.18s, color 0.18s;
}

.gallery-btn:hover,
.gallery-btn.active {
  background: var(--global-theme-color);
  color: var(--global-hover-text-color);
}

/* ── Masonry grid ───────────────────────────────────────── */
.gallery-grid {
  column-count: 3;
  column-gap: 0.75rem;
}

@media (max-width: 768px) { .gallery-grid { column-count: 2; } }
@media (max-width: 480px) { .gallery-grid { column-count: 1; } }

/* ── Cards ──────────────────────────────────────────────── */
.gallery-card {
  break-inside: avoid;
  margin-bottom: 0.75rem;
  border-radius: 8px;
  overflow: hidden;
  position: relative;
  background: var(--global-card-bg-color, #1a1a1a);
  box-shadow: 0 2px 8px rgba(0,0,0,0.25);
  transition: transform 0.2s, box-shadow 0.2s;
}

.gallery-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(0,0,0,0.35);
}

.gallery-img {
  width: 100%;
  display: block;
  cursor: zoom-in;
}

/* ── Caption overlay ────────────────────────────────────── */
.gallery-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 0.5rem 0.75rem;
  font-size: 0.75rem;
  color: #fff;
  background: linear-gradient(transparent, rgba(0,0,0,0.65));
  text-align: center;
  opacity: 0;
  transition: opacity 0.2s;
}

.gallery-card:hover .gallery-caption {
  opacity: 1;
}
</style>
