{% from "./schema-prop.rst" import schemaProp %}

{% macro schema(schema, schemaName, hideTitle=false) %}
{%- if not hideTitle -%}

{{ schemaName | generateHeader('"') }}

{% endif %}

.. list-table:: Parameter ``{{schemaName}}``
   :header-rows: 1

   * - Name
     - Type
     - Description
     - Accepted values
    {%- for propName, prop in schema.properties() -%}
        {{ schemaProp(prop, propName, required=(schema | isRequired(propName)), path='') }}
    {%- else -%}
        {{ schemaProp(schema, schemaName,  path='') }}
    {% endfor -%}

{% endmacro %}
