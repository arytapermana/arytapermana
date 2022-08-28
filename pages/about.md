---
layout: page
title: About
permalink: /about/
weight: 3
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:,<br>
Someone who is interested in video editing and design, sometimes web development is also my free time to do some experiments. I really like ideas and challenges that can advance self-development and even the world.

{% include elements/button.html link="https://www.behance.net/aryta" text="Behance" style="primary" size="sm" %}
{% include elements/button.html link="https://dribbble.com/aryaputra" text="Dribbble" style="primary" size="sm" %}
{% include elements/button.html link="https://www.linkedin.com/in/arytapermana" text="LinkedIn" style="primary" size="sm" %}
{% include elements/button.html link="https://drive.google.com/file/d/11n19CN28qv8PwIlUfPTw-sXK9xtdj62w/view?usp=sharing" text="CV" style="primary" size="sm" %}

<div class="row">
{% include about/skills.html title="Video Editor" source=site.data.video-editing-skills %}
{% include about/skills.html title="Graphics Design" source=site.data.graphics-design-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
</div>

<div class="row">
{% include about/timeline.html %}
</div>
