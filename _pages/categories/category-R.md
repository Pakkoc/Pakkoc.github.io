---
title: "R"
layout: archive
permalink: categories/R
author_profile: true
sidebar:
  nav: "docs"
---


{% assign posts = site.categories.R %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}