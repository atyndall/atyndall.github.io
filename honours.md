---
layout: page
permalink: /honours/
title: Honours
description: "Information regarding Ash's honours project."
---

Ash commenced his Honours project in July 2014, and is expected to finish around the same time in 2015.

He is publishing his thesis under a Creative Commons license. A copy of his thesis can be found on [Github](https://github.com/atyndall/honours).

He is also publishing the code related to the thesis under the GNU GPL. A copy of that can also be found on [Github](https://github.com/atyndall/thing).

He also writes about it on his blog. Posts about it are listed below; 

{% for tag in site.tags %}
{% if tag[0] == "honours" %}
<ul class="post-list">
{% assign pages_list = tag[1] %}  
{% for post in pages_list %}
{% if post.title != null %}
{% if group == null or group == post.group %}
<li><a href="{{ post.url }}">{{ post.title }}<span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span></a></li>
{% endif %}
{% endif %}
{% endfor %}
{% assign pages_list = nil %}
{% assign group = nil %}
</ul>
{% endif %}
{% endfor %}
