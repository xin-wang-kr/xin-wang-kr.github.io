---
layout: archive
permalink: /research/
title: "Projects"
author_profile: true
header:
  og_image: "posts/spatial-sql/gadm_wkt_filter_buffer-1.png"
---

{% include base_path %}
{% capture written_year %}'None'{% endcapture %}
{% for post in site.research %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year != written_year %}
    <h2 id="{{ year | slugify }}" class="archive__subtitle">{{ year }}</h2>
    {% capture written_year %}{{ year }}{% endcapture %}
  {% endif %}
  {% include archive-single.html %}
{% endfor %}
