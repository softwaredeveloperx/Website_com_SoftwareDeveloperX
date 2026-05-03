---
layout: a_new_page_id
title: 'Daftar Artikel, secara simple'
permalink: /simple/
---

{% assign id_posts = site.posts | where: "lang", "id" %}
{% for post in id_posts %}

- [{{ post.judul }}]({{ post.url }}) — {{ post.date | date: "%d %B %Y" }}
  {% endfor %}
