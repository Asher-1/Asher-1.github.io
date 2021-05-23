---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if author.wechat %}
  You can also find my articles on <u><a href="{{author.wechat}}">my Wechat profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}

