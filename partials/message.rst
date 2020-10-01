{% from "./schema.rst" import schema %}
{% from "./tags.rst" import tags %}

{% macro message(msg) %}
{% if msg.summary() -%}
{{ msg.summary() }}

{% endif -%}
{%- if msg.description() -%}
{{ msg.description() | safe }}
{% endif -%}

{% if msg.headers() -%}
Headers
~~~~~~~

{{ schema(msg.headers(), 'Message Headers', hideTitle=true) }}

{% if msg | getHeadersExamples %}

{{ "Examples of headers"|generateHeader("~") }}

{% for ex in msg | getHeadersExamples -%}

.. highlight:: json

    {{ ex | dump(2) | safe | indent}}

{% endfor -%}
{% else -%}
Example of headers _(generated)_
................................

.. highlight:: json

    {{ msg.headers().json() | generateExample | safe | indent}}

{% endif %}
{% endif %}

{% if msg.payload() -%}
Payload
~~~~~~~

{{ schema(msg.payload(), 'Message Payload', hideTitle=true) }}

{% if msg | getPayloadExamples %}
Examples of payload
...................

{% for ex in msg | getPayloadExamples %}

.. highlight:: json

    {{ ex | dump(2) | safe | indent}}

{% endfor -%}
{% else -%}
Example of payload _(generated)_
................................

.. highlight:: json

    {{ msg.payload().json() | generateExample | safe | indent}}

{% endif -%}
{% endif -%}


{% if msg.hasTags() %}
Tags
~~~~

{{ tags(msg.tags()) }}
{% endif %}
{% endmacro %}
