---
title: Gallery
layout: page
permalink: /gallery.html
---

# Gallery

<div id="gallery">
{%- assign images-to-split = '' -%}
{%- assign alts-to-split = '' -%}
{%- for image in site.data.config-gallery -%}
    {% capture new-image %}{{ image.path | absolute_url }}{% unless forloop.last %}{% cycle ';', '|' %}{% endunless %}{% endcapture %}
    {%- assign images-to-split = images-to-split | append: new-image -%}
{%- endfor -%}
{%- for image in site.data.config-gallery -%}
    {% capture new-alt %}{{ image.alt }}{% unless forloop.last %}{% cycle ';', '||' %}{% endunless %}{% endcapture %}
    {%- assign alts-to-split = alts-to-split | append: new-alt -%}
{%- endfor -%}

{%- assign image-groups = images-to-split | split: '|' -%}
{%- assign alt-groups = alts-to-split | split: '||' -%}
{%- for group in image-groups -%}
    {%- assign alts = alt-groups[forloop.index0] -%}
    {% include feature/image.html objectid=group alt=alts %}
{%- endfor -%}
</div>
