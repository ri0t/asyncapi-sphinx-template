{{(asyncapi.info().title() + " " + asyncapi.info().version() + " documentation")|generateHeader("#", true)}}

{% if asyncapi.info().ext('x-logo') -%}
![{{asyncapi.info().title()}} logo]({{asyncapi.info().ext('x-logo')}})
{% endif -%}

{% if asyncapi.info().description() -%}{{ asyncapi.info().description() | safe }}
{% endif -%}


Table of Contents
*****************

{% if asyncapi.info().termsOfService() -%}
* :ref:`terms_of_service`
{% endif -%}
{% if asyncapi.hasServers() -%}
* :ref:`servers`
{% endif -%}
{% if asyncapi.hasChannels() -%}
* :ref:`channels`
{% endif -%}

{% include "partials/content.rst" %}
