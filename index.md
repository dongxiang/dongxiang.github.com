---
layout: page
title: �����б�
tagline: �Ƽ���/������/mobile �������
---
{% include JB/setup %}



## Recents Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

����������� <a href="http://www.weibo.com/totheeast">������</a>��


