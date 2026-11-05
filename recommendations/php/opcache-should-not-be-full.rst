OPcache should not be full
==========================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

OPcache is full when its hash table has no key left, as configured by
`opcache.max_accelerated_files`_, or when less than 64 KB of its shared memory,
as configured by `opcache.memory_consumption`_, is free. From then on, OPcache
stops caching new scripts, and PHP compiles every script missing from the cache
on every request.

OPcache only empties and rebuilds the whole cache when its wasted memory reaches
`opcache.max_wasted_percentage`_, so a full cache usually stays full until PHP
restarts. Increase ``opcache.memory_consumption`` or
``opcache.max_accelerated_files`` so that every script of your application fits
in the cache.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.max_accelerated_files`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-accelerated-files
.. _`opcache.memory_consumption`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.memory-consumption
.. _`opcache.max_wasted_percentage`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-wasted-percentage
