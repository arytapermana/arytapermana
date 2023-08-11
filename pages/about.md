---
layout: page
title: About
permalink: /about/
weight: 3
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:,<br>
If you never know me, I'm just a regular guy like others but interested in internet culture and everything I like. I think you will know more about me below.

so don't be judged, you are free to learn more about me.

{% include elements/button.html link="https://www.behance.net/aryta" text="Behance" style="primary" size="sm" %}
{% include elements/button.html link="https://dribbble.com/aryaputra" text="Dribbble" style="primary" size="sm" %}
{% include elements/button.html link="https://www.linkedin.com/in/arytapermana" text="LinkedIn" style="primary" size="sm" %}
{% include elements/button.html link="https://www.instagram.com/arylupita/" text="Instagram" style="primary" size="sm" %}

<div class="row">
{% include about/skills.html title="UI/UX" source=site.data.uiux-skills %}
{% include about/skills.html title="Graphics" source=site.data.graphics-design-skills %}
{% include about/skills.html title="Video" source=site.data.video-editing-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
</div>

<div class="row">
{% include about/timeline.html %}
</div>
