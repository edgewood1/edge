---
layout: page
title: Category
permalink: /category/
published: true
default: category
---

Your categories
{% assign my_array = "" | split: ',' %}
 
<ul>
{% for post in site.posts %}

  {% unless my_array contains post.categories %}
  <li>
     <a href="{{post.categories}}">{{ post.categories }}</a>
  </li>
     <!-- <p>{{ post.meta }}</p> -->
     {% assign my_array = my_array | push: post.categories %}
    
     {% endunless %}
{% endfor %}
</ul>