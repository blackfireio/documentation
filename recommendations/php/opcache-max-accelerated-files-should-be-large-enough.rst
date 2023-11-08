"opcache.max_accelerated_files" should be large enough
======================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

The `opcache.max_accelerated_files`_ ini setting configures the maximum number
of files that can be cached. Complex applications involve a lot of different
PHP files, so it's recommended to increase the default value of
``opcache.max_accelerated_files`` in production.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.max_accelerated_files`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-accelerated-files
