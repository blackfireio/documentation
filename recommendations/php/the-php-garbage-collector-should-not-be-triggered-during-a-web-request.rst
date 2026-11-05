The PHP garbage collector should not be triggered during a Web request
======================================================================

The `PHP Garbage Collector`_ process may introduce a performance overhead to your
applications. PHP triggers it automatically once around 10,000 possible roots,
the arrays and objects that may belong to a reference cycle, are waiting in its
buffer. Since PHP 7.3, this threshold grows by 10,000 each time a collection
frees fewer than 100 values, and goes back down when collections free more.

Blackfire counts both the automatic collections and the calls to
`gc_collect_cycles()`_, so calling this function during a web request also
fails this recommendation.

Creating that many possible roots during a web request is a rare edge case that
should be avoided by moving that heavy processing to a background task. In case
it's not possible to do that, you should call the `gc_disable()`_ function before
processing that complex web request.

See also the official PHP doc, which gives useful `performance considerations`_ related to the garbage collector.

.. _`PHP Garbage Collector`: https://www.php.net/manual/en/features.gc.collecting-cycles.php
.. _`gc_collect_cycles()`: https://www.php.net/manual/en/function.gc-collect-cycles.php
.. _`gc_disable()`: https://www.php.net/manual/en/function.gc-disable.php
.. _`performance considerations`: https://www.php.net/manual/en/features.gc.performance-considerations.php
