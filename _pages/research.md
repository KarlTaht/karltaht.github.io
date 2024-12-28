---
layout: archive
title: "Research"
permalink: /research/
---
## University Research

Back in the Utah Architecture lab, my main research project focused on software and systems. My thesis centralizes around program phase detection and both hardware and software performance optimization, all with a machine learning flavor. Through my research, I’ve had the opportunity to intern with Intel Labs twice were I worked on these problems from a hardware engineer’s perspective. More recently, I have shifted my focus towards warehouse scale performance optimization. I recently completed an internship at Facebook with the Warehouse Java Efficiency team, where I plans to join full-time in 2020. 

<!-- ## Publications

It takes a lot of foundational learning to get to where you ultimately like what you do. Below you'll find my publications -->

## [Research Paper Summaries](/research-papers/)

Since 2018, I've been summarizing every research paper I read. I find this helps
me remember works better, and recall them when I need to find relevant work. I'm
currently migrating those posts into this new GitHub-based site. Below you'll find the most recent papers I've read and summarized.


{% for post in site.categories.research %}
  {% include archive-single.html %}    
{% endfor %}