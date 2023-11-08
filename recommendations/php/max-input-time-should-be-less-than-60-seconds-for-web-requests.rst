"max_input_time" should be less than 60 seconds for Web requests
================================================================

The `max_input_time`_ ini setting defines the maximum time in seconds a script
is allowed to parse input request data, like POST and GET.

The pool of running PHP threads is limited and increasing this value may result
in reaching this limit more easily, turning your server into an easy target for
`denial of service attacks`_.

It's strongly recommended to reduce this setting in your ``php.ini``
configuration using ``max_input_time=60``.

.. _`max_input_time`: https://www.php.net/manual/en/info.configuration.php#ini.max-input-time
.. _`denial of service attacks`: https://en.wikipedia.org/wiki/Denial-of-service_attack
