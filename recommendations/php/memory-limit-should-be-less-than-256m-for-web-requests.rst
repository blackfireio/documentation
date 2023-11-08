"memory_limit" should be less than 256M for Web requests
========================================================

The `memory_limit`_ ini setting controls the maximum memory a PHP script
can allocate. This limit should be low for each PHP script so that more
concurrent requests can be processed by the server.

If the server memory is completely full, the whole system will slow down, making
your server an easy target for `denial of service attacks`_.

It's strongly recommended to reduce this setting in your ``php.ini``
configuration using ``memory_limit=256M``.

.. _`memory_limit`: https://www.php.net/manual/en/ini.core.php#ini.memory-limit
.. _`denial of service attacks`: https://en.wikipedia.org/wiki/Denial-of-service_attack
