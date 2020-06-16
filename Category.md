---
layout: page
title: Categories
---

<header class="site-category">
  <ul>
    {% assign pages_list = site.pages %} {% for node in pages_list %} {% if
    node.title != null %} {% if node.layout == "category" %}
    <li>
      <a
        class="category-link {% if page.url == node.url %} active{% endif %}"
        href="{{ site.baseurl }}{{ node.url }}"
        >{{ node.title }}</a
      >
    </li>
    {% endif %} {% endif %} {% endfor %}
  </ul>
</header>

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>

    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
    </article>
    {% endfor %}

  </div>
{% endfor %}
</div>
