---
layout: page
ref: categories
lang: en
permalink: /categories-en/
alt-title: Categories
---

<ul class="social-media-list">
{% assign pages=site.pages | where:"ref", page.ref | sort: 'lang' %}
{% for entry in pages %}
  <li>
    {% if entry.lang == page.lang %}
    <a href="{{ entry.url }}" class="{{ entry.lang }}"><b>{{ entry.lang }}</b></a>
    {% else %}
    <a href="{{ entry.url }}" class="{{ entry.lang }}">{{ entry.lang }}</a>
    {% endif %}
  </li>
{% endfor %}
</ul>    

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>

    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    {% if post.lang == page.lang %}
    <article class="archive-item">
      <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}} </a></h4>
    </article>
    {% endif %}
    {% endfor %}
  </div>
{% endfor %}
</div>