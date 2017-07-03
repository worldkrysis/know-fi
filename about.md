---
layout: page
permalink: /about/index.html
title: About the Author
tags: [about, krystian, zawodniak, authors]
chart: true
---
{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}


<div class="about">
  <img class="about" src="{{ site.url }}/images/avatar.jpg" alt="Author photo: Krystian Zawodniak">
  <p class="about">
  Krystian Zawodniak, Founder
  </p>
</div>


**know-fi** is a music-blog dedicated to writing music reviews without using a linear rating systems (ex. 0-10).

Rather than describing songs as having *[warm synth tones](https://youtu.be/ZGMALkWKKaw?t=114)*, know-fi will help readers understand why songs sound the way they sound. Alongside album reviews, know-fi writes about trends in the music industry, as well as other music-related opinion pieces.

Krystian (based out of Boston, MA) has launched this project to learn more about the music he loves, as well as practice building a website. Check out [this site's GitHub repository](https://github.com/worldkrysis/know-fi).

**know-fi** currently has {{ site.posts | size }} posts in {{ site.categories | size }} categories which combinedly have {{ total_words }} words, which will take an average reader ({{ site.wpm }} WPM) approximately <span class="time">{{ total_readtime }}</span> minutes to read. {% if featuredcount != 0 %}There are <a href="{{ site.url }}/featured">{{ featuredcount }} featured posts</a>, you should definitely check those out.{% endif %} The most recent post is {% for post in site.posts limit:1 %}{% if post.description %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}">"{{ post.title }}"</a>{% else %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}" title="Read more about {{ post.title }}">"{{ post.title }}"</a>{% endif %}{% endfor %} which was published on {% for post in site.posts limit:1 %}{% assign modifiedtime = post.modified | date: "%Y%m%d" %}{% assign posttime = post.date | date: "%Y%m%d" %}<time datetime="{{ post.date | date_to_xmlschema }}" class="post-time">{{ post.date | date: "%d %b %Y" }}</time>{% if post.modified %}{% if modifiedtime != posttime %} and last modified on <time datetime="{{ post.modified | date: "%Y-%m-%d" }}" itemprop="dateModified">{{ post.modified | date: "%d %b %Y" }}</time>{% endif %}{% endif %}{% endfor %}.
