---
name: tasdik
tools: [java, test]
image: https://www.sketchappsources.com/resources/source-image/project-neon-groove-music-ui.png
description: Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
#external_url: https://www.google.com
---

just fucking test

- a
- b
- c
- d
- e
- f
- g




{%- capture list_items -%}
Google,https://www.google.com
GitHub,https://www.google.com
{%- endcapture -%}

{% include elements/list.html %}


{% include elements/video.html id="aZNbUITN-mA" %}

{% include elements/figure.html image="https://bit.ly/2N69TKO" caption="The sea complains upon a thousand shores." %}

{% include elements/button.html link="https://github.com/" text="GitHub" %}
{% include elements/button.html link="https://github.com/" text="GitHub" style="primary" %}
{% include elements/button.html link="https://github.com/" text="GitHub" style="outline-dark" %}

<p class="text-center"> {% include elements/button.html link="https://github.com/" text="GitHub" %} {% include elements/button.html link="https://google.com/" text="Google" %} {% include elements/button.html link="https://microsoft.com/" text="Microsoft" style="outline-dark" %} </p>