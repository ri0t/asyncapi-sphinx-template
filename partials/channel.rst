{% from "./parameters.rst" import parameters %}
{% from "./operation.rst" import operation %}
{% macro channel(chan, channelName) %}

.. _{{channelName}}:

{{ channelName | generateHeader("=") }}

{% if chan.description() -%}
{{ chan.description() | safe }}
{% endif -%}

{% if chan.parameters() -%}
{{- parameters(chan.parameters()) -}}
{% endif -%}

Messages
--------
{%- if chan.hasPublish() -%}
{{ operation(chan.publish(), channelName) }}
{%- endif -%}
{%- if chan.hasSubscribe() -%}
{{ operation(chan.subscribe(), channelName) }}
{%- endif -%}
{% endmacro %}
