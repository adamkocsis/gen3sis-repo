---
title: Examples for simulation access
layout: page
show_sidebar: false
permalink: /example/
---


<div>

The actual files could be hosted on Zenodo. The trial files are put on the Zenodo sandbox.

{% for sim in site.data.simulations %}
<p>
{{sim.simulation}} -  <a href="{{sim.space_link}}">{{sim.space}}</a> - <a href="{{sim.config_link}}">{{sim.config}}</a>
</p>

{% endfor %}
</div>

<div markdown="1">
- This is an imaginary table! :)
- There can be a static page generated for every paper, where you could see all available inputs for the paper.
- Those pages can have specific chronosphere `fetch` statements

</div>

