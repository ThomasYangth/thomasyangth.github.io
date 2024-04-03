---
layout: archive
title: "Selected Publications"
permalink: /publications/
author_profile: true
---


The following is a selected list of my publications as of March 2024.

You can also find my articles on <a href="https://scholar.google.com/citations?user=MXF9R18AAAAJ&hl=en">my Google Scholar profile page</a>.

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
