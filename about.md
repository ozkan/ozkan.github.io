---
layout: basic
title: 
date: 
description:  Özkan Çelik
#img: about_us.png # Add image post (optional)
tags: # add tag
type: about
disqus_disabled: true
permalink: /about/

---

{% assign colors = 'red|green|blue|yellow|orange' | split: '|' %}
{% for i in (1..100) %}
  {{ i }} - {{ forloop.index | random_item: colors }}
{% endfor %}