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

<!-- Category filter buttons -->
<div class="gallery-filter mb-4 text-center">
  <button class="btn btn-sm btn-outline-primary active mr-1 mb-1" data-filter="all">All</button>
  {%- for cat in categories %}
  <button class="btn btn-sm btn-outline-primary mr-1 mb-1" data-filter="{{ cat }}">
    {{ cat | capitalize }}
  </button>
  {%- endfor %}
</div>

<!-- Masonry gallery grid -->
<div class="grid">
  {%- for photo in photos %}
  {%- assign src_path = photo.file | prepend: "/" | prepend: photo.category | prepend: "assets/img/gallery/" %}
  {%- assign alt_text = photo.alt | default: photo.caption | default: photo.file %}
  <div class="grid-item gallery-item" data-category="{{ photo.category }}">
    <figure>
      <img
        src="{{ src_path | relative_url }}"
        alt="{{ alt_text }}"
        class="img-fluid rounded z-depth-1 gallery-img"
        data-zoomable
        loading="lazy"
      >
      {%- if photo.caption %}
      <figcaption class="caption mt-1 text-center text-muted" style="font-size:0.8rem;">
        {{ photo.caption }}
      </figcaption>
      {%- endif %}
    </figure>
  </div>
  {%- endfor %}
</div>

<!-- Filter & layout script -->
<script>
document.addEventListener('DOMContentLoaded', function () {
  var buttons = document.querySelectorAll('.gallery-filter button');
  var items   = document.querySelectorAll('.gallery-item');

  buttons.forEach(function (btn) {
    btn.addEventListener('click', function () {
      buttons.forEach(function (b) { b.classList.remove('active'); });
      btn.classList.add('active');

      var filter = btn.getAttribute('data-filter');
      items.forEach(function (item) {
        item.style.display =
          (filter === 'all' || item.getAttribute('data-category') === filter)
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
.grid { width: 100%; }
.grid-item {
  width: calc(33.333% - 10px);
  margin-bottom: 10px;
}
@media (max-width: 768px) { .grid-item { width: calc(50% - 10px); } }
@media (max-width: 480px) { .grid-item { width: 100%; } }

.gallery-img { width: 100%; cursor: zoom-in; display: block; }

.gallery-filter .btn.active {
  color: #fff;
  background-color: var(--global-theme-color);
  border-color: var(--global-theme-color);
}
</style>
