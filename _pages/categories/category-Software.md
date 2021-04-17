---
title: "Software"
layout: archive
permalink: categories/software
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.software %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}