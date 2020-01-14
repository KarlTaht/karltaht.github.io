---
layout: archive
title: "Reality"
permalink: /reality/
---

While this site has a few very focused sections, such as my research paper 
summaries, there's a lot of things I feel are worth writing down but don't fall
into some particular category, other than that they are life, they are reality.

{% for post in site.categories.reality %}
  - [{{ post.title }}]({{ post.url }}) 

    {{post.custom_excerpt}}
    
    Published on <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
    
{% endfor %}