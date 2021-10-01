---
title: "Boostcamp Dairy"
layout: archive
permalink: categories/ai-boostcamp
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['AI Boostcamp'] %}
{% for post in posts %} {% include archive-double.html type=page.entries_layout %} {% endfor %}