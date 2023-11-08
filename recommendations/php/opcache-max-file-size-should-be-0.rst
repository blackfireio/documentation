"opcache.max_file_size" should be 0
===================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

The `opcache.max_file_size`_ ini setting defines the maximum file size in bytes
allowed by OPcache. If the original file is larger than that size, it won't be
cached. This means that those files must be loaded and compiled repeatedly for
every request, introducing a significant impact in your application performance.

Disable this setting using ``opcache.max_file_size=0`` (``0`` means unlimited
file size) or remove this setting (since ``0`` is the default value).

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.max_file_size`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.max-file-size
