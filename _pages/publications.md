---
layout: page
permalink: /publications/
title: Publications
description: Publications by the group members
years: [2023, 2022, 2021, 2020, 2019, 2018, 2017]
nav: true
nav_rank: 5
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{y}}]* %}
{% endfor %}

</div>
