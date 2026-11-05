OPcache should not restart when it is full
==========================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

When OPcache is full, either because its hash table has no key left
(`opcache.max_accelerated_files`_) or because its shared memory is exhausted
(`opcache.memory_consumption`_), and its wasted memory reaches
`opcache.max_wasted_percentage`_, OPcache empties the whole cache. PHP then
compiles every script again, which slows down the requests that follow the
restart.

Increase ``opcache.memory_consumption`` or ``opcache.max_accelerated_files`` so
that every script of your application fits in the cache.

PHP only resets the restart counters when it creates the OPcache shared memory,
so this recommendation keeps failing until PHP restarts, even after you fix the
configuration.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.max_accelerated_files`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-accelerated-files
.. _`opcache.memory_consumption`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.memory-consumption
.. _`opcache.max_wasted_percentage`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-wasted-percentage
