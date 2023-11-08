"opcache.enable_file_override" should be enabled
================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

When the `opcache.enable_file_override`_ ini setting is enabled, OPcache is used
when calling ``file_exists()``, ``is_file()`` and ``is_readable()``. This
improves your application performance by saving some calls to stat those files,
which is specially significant for class autoloaders.

Enable this setting in production using ``opcache.enable_file_override=1``.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.enable_file_override`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.enable-file-override
