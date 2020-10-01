{% from "./channel.rst" import channel %}

.. _channels:

Channels
********

All declared channels:

{% for channelName, chan in asyncapi.channels() -%}
* :ref:`{{channelName}}`
{% endfor -%}

{% for channelName, chan in asyncapi.channels() -%}
{{ channel(chan, channelName) }}
{% endfor -%}
