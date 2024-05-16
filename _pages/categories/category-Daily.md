---
title: "Daily"
layout: archive
permalink: categories/Daily
author_profile: true
sidebar:
  nav: "docs"
---


{% assign posts = site.categories.Daily %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}