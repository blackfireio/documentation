"opcache.consistency_checks" should not be enabled
==================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

When the `opcache.consistency_checks`_ ini setting is greater than 0, the
checksums of the OPcache contents are verified every N requests, impacting your
application performance.

This option should only be enabled when debugging and it must be disabled in
production. Disable this setting using ``opcache.consistency_checks=0`` or
remove this setting (since ``0`` is the default value).

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`opcache.consistency_checks`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.consistency-checks
