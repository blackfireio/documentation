"max_execution_time" should be less than 30 seconds for Web requests
====================================================================

The `max_execution_time`_ ini setting defines the maximum time in seconds a
script is allowed to run before it is automatically terminated.

The pool of running PHP processes is limited and increasing this value may
result in exhausting the pool more easily, turning your server into an easy
target for `denial of service attacks`_.

Sometimes, requests take more time than the limit because they compute complex
tasks like exporting a whole database table. In those cases, it's better to
offload the PHP request from that complex task and execute the task
asynchronously using a background job worker.

It's strongly recommended to reduce this setting in your ``php.ini``
configuration using ``max_execution_time=30``.

.. _`max_execution_time`: https://www.php.net/manual/en/info.configuration.php#ini.max-execution-time
.. _`denial of service attacks`: https://en.wikipedia.org/wiki/Denial-of-service_attack
