---
layout: fieldnotes
title: Field Notes from the step pyramid
permalink: /fieldnotes/
---

<div class="row listrecent">
{% for category in site.categories %}

<!-- Field Notes Posts -->

{% if category[0] == "FieldNotes" %}

<div class="section-title col-md-12 mt-4">
<h2 id="{{ category[0] | replace: " ","-" }}">All <span class="text-capitalize">Field Notes</span></h2>
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
