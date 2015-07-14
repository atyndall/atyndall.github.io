---
layout: page
permalink: /honours/
title: Honours
description: "Information regarding Ash's honours project."
---

Ash commenced his Honours project in July 2014 and submitted his thesis in May 2015.

The focus of Ash's research was occupancy detection, specifically, determining the number of people in a given area in a low-cost, reliable, non-invasive and energy efficient way.

This has a variety of applications, with Ash's focus being on its uses in a "smart-home for the disabled"​; a larger system equipped with a variety of assistive technologies designed to improve quality of life for occupants in a variety of ways.

Ash was praised for his research skills and the breadth and depth of his inquiry. An examiner wrote; "There is not a lot to say about Ash Tyndall's project and resulting thesis; they are superb."​ [Read full letter](MichaelWiseFeedback.pdf).

The most accessible explanation of Ash's research is the research poster he prepared for the School of Computer Science;

<figure>
  <a href="poster.pdf"><img src="poster.png" /></a>
  <figcaption><a href="poster.pdf">Research Poster (click to enlarge)</a></figcaption>
</figure>

A more in-depth, but still accessible, explanation of Ash's work can be found in his seminar presentation slides;

<figure>
  <a href="presentation.pdf"><img src="presentation.png" /></a>
  <figcaption><a href="presentation.pdf">Seminar Presentation Slides (click to view)</a></figcaption>
</figure>

Finally, if you want the whole story, you can read his thesis [here](thesis.pdf).

The thesis is published under a Creative Commons license. A copy of the source code can be found on [Github](https://github.com/atyndall/honours)

The related code is published under the GNU GPL. A copy of that can also be found on [Github](https://github.com/atyndall/thing).

<br>

He also wrote about the experience on his blog. Posts about it are listed below; 

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
