{% from "./message.rst" import message %}

{% macro operation(op, channelName) %}
{% set summary = op.summary() %}

{% set header = "``unknown``" %}
{% if op.isPublish() %}{% set header = "``publish`` " %}
{% elseif op.isSubscribe() %}{% set header = "``subscribe`` " %}
{% endif %}
{% set header = header + channelName %}

{{- header | generateHeader('^') }}

{% if summary -%} *{{ summary }}* {% endif -%}

{{ op.description() }}

{{ ("Message ``" + op.id() + "``") | generateHeader("+") }}

{% if op.hasMultipleMessages() -%}
Accepts **one of** the following messages:

{% for msg in op.messages() -%}
{{ ("Message " + msg.uid()) | generateHeader('+') -}}

{{ message(msg) }}
{% endfor -%}
{%- else -%}
{{ message(op.message(0)) }}
{%- endif -%}
{% endmacro %}
