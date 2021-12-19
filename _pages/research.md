---
layout: archive
title: "Projects"
permalink: /research/
author_profile: true
---

My research 
<nbsp>

{% include base_path %}

{% assign ordered_pages = site.research %}

{% for post in ordered_pages %}
  {% include archive-single.html type="grid" %}
{% endfor %}
