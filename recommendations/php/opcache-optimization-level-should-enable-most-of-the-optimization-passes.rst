"opcache.optimization_level" should enable most of the optimization passes
==========================================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

The `opcache.optimization_level`_ ini setting is a bitmask that controls which
optimization passes are executed for the scripts. Keep every pass enabled by the
PHP default value, ``0x7FFEBFFF`` since PHP 7.3 and ``0x7FFFBFFF`` before, as
the recommendation fails when one of the `OPcache optimizations`_ 1 to 14 or 16
("Inline functions") is disabled. Pass 15 ("Collect constants") is unsafe and
stays off by default.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`OPcache optimizations`: https://github.com/php/php-src/blob/master/Zend/Optimizer/zend_optimizer.h
.. _`opcache.optimization_level`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.optimization-level
