{% include "partials/info.rst" %}

{% if asyncapi.hasChannels() -%}
{% include "partials/channels.rst"  %}
{% endif -%}
