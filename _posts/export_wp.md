---
---

<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  {% for post in site.posts %}
    <entry>
      <title type="html">{{ post.title | xml_escape }}</title>
      <link href="{{ site.url }}{{ post.url }}" />
      {% assign slug_to_remove = post.url | slice: 0, 12 %}
      {% assign sliced_slug = post.slug | remove_first: slug_to_remove %}
      <slug>{{ sliced_slug }}</slug>
      
      <id>{{ site.url }}{{ post.id }}</id>
      <summary type="html">{{ post.content | strip_html | truncatewords: 50 | xml_escape }}</summary>
      <content type="html">{{ post.content | xml_escape }}</content>
      <author>
        {% if post.author %}
          <name>Zoran</name>
        {% else %}
          <name>Zoran</name>
        {% endif %}
      </author>
      <category>{{ post.category }}</category>
      <tags>{{ post.tags | join: "," }}</tags>
    </entry>
  {% endfor %}
</feed>
