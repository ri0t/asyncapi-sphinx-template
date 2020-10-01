
Meta
****

{% if asyncapi.info().termsOfService() -%}

.. _terms_of_service:

Terms of service
================
[{{asyncapi.info().termsOfService()}}]({{asyncapi.info().termsOfService()}})
{% endif -%}

{% if asyncapi.hasServers() %}

.. _servers:

Servers
=======

.. list-table:: Servers
   :header-rows: 1

   * - URL
     - Protocol
     - Description
{%- for serverName, server in asyncapi.servers() %}
   * - {{server.url()}}
     - {{server.protocol()}}{% if server.protocolVersion() %}{{server.protocolVersion()}}{% endif %}
     - {{server.description()}}
{%- endfor %}

Variables
---------

{%- for serverName, server in asyncapi.servers() %}
{% if server.variables() | length > 0 -%}

.. list-table:: Variables for Server ``{{serverName}}``
   :header-rows: 1

   * - Name
     - Default value
     - Possible values
     - Description
   {% for varName, var in server.variables() -%}
   * - {{varName}}
     - {% if var.hasDefaultValue() %}{{var.defaultValue()}}{% else %}*None*{% endif %}
     - {% if var.hasAllowedValues() %}{%- for value in var.allowedValues() %}{{value}}, {%- endfor -%}{% else %}Any{% endif %}
     - {{ var.description() | safe }}
     {% endfor -%}
{% endif %}
{%- endfor -%}

Security
--------

{%- for serverName, server in asyncapi.servers() %}
{% if server.security() | length > 0-%}

.. list-table::  Security Requirements for Server ``{{serverName}}``
   :header-rows: 1

   * - Type
     - In
     - Name
     - Scheme
     - Format
     - Description
   {%- for security in server.security() %}
   {% set def = asyncapi.components().securityScheme(security.json() | keys | head ) %}
   * - {{def.type()}}
     - {{def.in()}}
     - {{def.name()}}
     - {{def.scheme()}}
     - {{def.bearerFormat()}}
     - {{def.description() | safe }}
   {%- endfor -%}
{% endif %}
{%- endfor -%}

{% endif -%}
