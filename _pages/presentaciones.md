---
layout: archive
permalink: /presentaciones/
excerpt: "Hablando de TIG..."
title: "Presentaciones"
author_profile: true
header:
  overlay_image: /images/pages/yopresentaciones.png
  overlay_filter: 0.1 # same as adding an opacity of 0.5 to a black background
---

{% include base_path %}
{% include group-by-array collection=site.posts field="categories" %}

{% for category in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  {% for post in posts %}
    {% if post.categories contains "Presentaciones" %}
      {% include archive-single.html %}
    {% endif %}
  {% endfor %}
{% endfor %}
