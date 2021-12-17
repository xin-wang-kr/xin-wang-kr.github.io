---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
classes: wide
---

Clicking on any of the links to see more details on the projects.

{% include base_path %}

{% for post in site.projects reversed %}
  {% include archive-single.html %}
{% endfor %}
