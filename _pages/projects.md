---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
classes: wide
images: 
  - image: /images/research/face-mask/correct-mask-1.jpg
  - image: /images/research/face-mask/mask-type-1.png
  - image: /images/research/face-mask/mask-type-2.png
---
{% include base_path %}

# [Face Mask Detection](projects/face-mask.md)
<p float="left">
  <img src="/images/research/face-mask/correct-mask-1.jpg" height="150" width="200" />
  <img src="/images/research/face-mask/mask-type-1.png" height="150" width="200" /> 
  <img src="/images/research/face-mask/mask-type-3.png" height="150" width="200" />
</p>

 {% assign images = {{page.images}} %}
    {% if images %}
    {% include carousel.html height="50" unit="%" duration="7" images= images %}
  {% endif %}`
