# d8_twig_tips
## Pass variable to the child paragraph
Some background description...

field-parent.html.twig

```twig
{% set hide_media = false %}
{% set has_image = false %}
{% set has_icon = false %}

{% for item in items if not hide_media %}

  {% set field_image = item.content['#paragraph'].field_paragraph_single.entity.field_image %}
  {% set field_icon = item.content['#paragraph'].field_paragraph_single.entity.field_icon %}

  {% if (field_image is empty) and (field_icon is empty) %}
    {% set hide_media = true %}
  {% endif %}
  {% if field_image %}
    {% set has_image = true %}
    {% if has_icon %}
      {% set hide_media = true %}
    {% endif %}
  {% endif %}
  {% if field_icon %}
    {% set has_icon = true %}
    {% if has_image %}
      {% set hide_media = true %}
    {% endif %}
  {% endif %}

{% endfor %}

{% for item in items %}
  {% set render = item.content %}
  {% set render = render|merge( { "#hide_media": hide_media } ) %}
  {{ render }}
{% endfor %}
```
