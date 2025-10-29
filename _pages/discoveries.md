---
layout: page
permalink: /discoveries/
title: Discoveries
description: Newly discovered pulsars from COMPACT searches.
nav: true
nav_rank: 6
---

{% assign rows = site.discoveries | sort: "discovered" | reverse %}
<table class="table table-bordered">
  <thead>
    <tr>
      <th>JNAME</th>
      <th>Cluster</th>
      <th>P0 (ms)</th>
      <th>DM (pc cm<sup>-3</sup>)</th>
      <th>Binary?</th>
      <th>Date of Discovery</th>
    </tr>
  </thead>
  <tbody>
  {% for d in rows %}
    <tr>
      <td><a href="{{ d.url | relative_url }}">{{ d.jname }}</a></td>
      <td>{{ d.cluster }}</td>
      <td>{{ d.p0_ms | round: 2 }}</td>
      <td>{{ d.dm | round: 3 }}</td>
      <td>{{ d.binary }}</td>
      <td>{{ d.discovered | date: "%d/%m/%Y" }}</td>
    </tr>
  {% endfor %}
  </tbody>
</table>


All globular cluster discoveries : [GC Pulsars](https://www3.mpifr-bonn.mpg.de/staff/pfreire/GCpsr.html).