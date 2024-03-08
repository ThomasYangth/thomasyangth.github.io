---
layout: archive
title: "Selected Publications"
permalink: /publications/
author_profile: true
---


The following is a selected list of my publications as of September 2023.

You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
