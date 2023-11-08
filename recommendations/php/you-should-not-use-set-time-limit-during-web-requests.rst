You should not use "set_time_limit()" during Web requests
=========================================================

In PHP applications, the `max_execution_time`_ setting defines the maximum time
in seconds a script is allowed to run before it is automatically terminated.
Scripts can modify this global setting with the `set_time_limit()`_ function.

You should not modify this setting because the number of processes that execute
PHP scripts on the server is limited and increasing the execution time of each
of them will exhaust the available processes. This will hurt the perceived
performance because the latency increases and it makes your server an easy
target for `denial of service attacks`_.

.. _`set_time_limit()`: https://www.php.net/manual/en/function.set-time-limit.php
.. _`max_execution_time`: https://www.php.net/manual/en/info.configuration.php#ini.max-execution-time
.. _`denial of service attacks`: https://en.wikipedia.org/wiki/Denial-of-service_attack
