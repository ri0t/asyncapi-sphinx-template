{% macro schemaTable(prop, propName, required=false, path='', circular=false) %}
   * - {{ path | tree }}{{ propName }} {% if required %}**(required)**{% endif %}
     - {{ prop.type() }}{%- if prop.anyOf() -%}anyOf{%- endif -%}{%- if prop.allOf() -%}allOf{%- endif -%}{%- if prop.oneOf() %}oneOf{%- endif -%}{%- if prop.items().type %}({{prop.items().type()}}){%- endif %}
     - {{ prop.description() | safe }} {% if circular %}**[CIRCULAR]**{% endif %}
     - {{ prop.enum() | acceptedValues | safe }}

{%- endmacro -%}
