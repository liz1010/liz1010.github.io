---
layout: archive
title: Archive
permalink: /archive
---
<h1 class="homepage">
  Archive
</h1>

<ul class="archive">
  {% for category in site.categories %}
    <li class="archive">
      {% capture category_name %}{{ category | first }}{% endcapture %}
      <a class="archive" name="{{ category_name | slugize }}">{{ category_name }}</a>
    </li>
  {% endfor %}
</ul>
