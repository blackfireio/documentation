The PHP garbage collector should not be triggered during a Web request
======================================================================

The `PHP Garbage Collector`_ process may introduce a performance overhead to your
applications. It's triggered automatically after creating (and keeping alive)
more than 10,000 objects in the same PHP process.

Creating 10,000 objects during a web request is a rare edge case that should be
avoided by moving that heavy processing to a background task. In case it's not
possible to do that, you should call the `gc_collect_cycles()`_ and `gc_disable()`_
functions before processing that complex web request.

See also the official PHP doc, which gives useful `performance considerations`_ related to the garbage collector.

.. _`PHP Garbage Collector`: https://www.php.net/manual/en/features.gc.collecting-cycles.php
.. _`gc_collect_cycles()`: https://www.php.net/manual/en/function.gc-collect-cycles.php
.. _`gc_disable()`: https://www.php.net/manual/en/function.gc-disable.php
.. _`performance considerations`: https://www.php.net/manual/en/features.gc.performance-considerations.php
