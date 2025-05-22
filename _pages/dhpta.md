---
layout: dhpta
title: DHPTA
permalink: /dhpta/
---

<div class="row listrecent">
{% for category in site.categories %}

<!-- DHPTA Posts -->

{% if category[0] == "DHPTA" %}

<div class="section-title col-md-12 mt-4">
<h2 id="{{ category[0] | replace: " ","-" }}"><span class="text-capitalize">DHPTA</span> Related Posts</h2>
</div>
{% assign pages_list = category[1] %}
{% for post in pages_list %}
{% if post.title != null %}
{% if group == null or group == post.group %}
{% include postbox.html %}
{% endif %}
{% endif %}
{% endfor %}
{% endif %}

<!-- DHPTA Datasets -->

{% if category[0] == "DHPTA dataset" %}

<div class="section-title col-md-12 mt-4">
<h2 id="{{ category[0] | replace: " ","-" }}"><span class="text-capitalize">Analyzed Datasets</span></h2>
</div>
{% assign pages_list = category[1] %}
{% for post in pages_list %}
{% if post.title != null %}
{% if group == null or group == post.group %}
{% include postbox.html %}
{% endif %}
{% endif %}
{% endfor %}
{% endif %}

{% endfor %}

</div>
