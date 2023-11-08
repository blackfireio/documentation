"opcache.optimization_level" should enable most of the optimization passes
==========================================================================

`OPcache`_ is a PHP extension that improves application performance by storing
precompiled script `opcodes`_ in shared memory. It removes the need to load,
parse and compile PHP files on every request.

The `opcache.optimization_level`_ ini setting is a bitmask that controls which
optimization passes are executed for the scripts. It's recommended to activate
all `OPcache optimizations`_ except passes 4 ("CFG based optimization") and 5
("DFA based optimization") that may be too slow for large files, and 15 ("Inline
functions") that may be buggy.

.. _`OPcache`: https://www.php.net/manual/en/book.opcache.php
.. _`opcodes`: https://en.wikipedia.org/wiki/Opcode
.. _`OPcache optimizations`: https://github.com/php/php-src/blob/master/ext/opcache/Optimizer/zend_optimizer.h
.. _`opcache.optimization_level`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.optimization-level
