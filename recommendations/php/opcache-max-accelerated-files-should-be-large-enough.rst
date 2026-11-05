"opcache.max_accelerated_files" should be large enough
======================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

The `opcache.max_accelerated_files`_ ini setting configures the size of the
OPcache hash table. PHP rounds it up to the next prime number of a fixed list,
``16229`` for the default ``10000``, and a script included through a relative
path uses one more key, so the table can fill up before the number of cached
scripts reaches the setting. Once the table is full, PHP stops caching new
scripts and compiles them on every request.

This recommendation fails when more than 85% of the keys are used. Complex
applications involve a lot of different PHP files, so it's recommended to
increase the default value of ``opcache.max_accelerated_files`` in production.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.max_accelerated_files`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-accelerated-files
