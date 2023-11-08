"opcache.file_cache_only" should not be enabled
===============================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

When the `opcache.file_cache_only`_ ini setting is enabled, OPcache no longer
caches the opcodes and it only stores the content of the scripts, impacting your
application performance.

Disable this setting using ``opcache.file_cache_only=Off`` or remove this
setting (since ``Off`` is the default value).

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.file_cache_only`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.file-cache-only
