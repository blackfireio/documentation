The session garbage collector should be disabled in production
==============================================================

The `session.gc_probability`_ and `session.gc_divisor`_ settings are used by PHP
to define the probability of starting the session garbage collection process
before any session initialization.

The garbage collection process is a blocking process, meaning that when it
starts, the current request must wait until the recollection finishes. This
behavior may impact the performance as perceived by end users.

It's recommended to disable the garbage collection process for sessions in your
``php.ini`` configuration using ``session.gc_probability=0`` and use a Cron job
instead to remove the expired sessions using the `session_gc()`_ method. Here
is such an example from the PHP documentation:

.. code-block:: php

    // Note: This script should be executed by the same user of web server process.

    // Need active session to initialize session data storage access.
    session_start();

    // Executes GC immediately
    session_gc();

    // Clean up session ID created by session_gc()
    session_destroy();

.. _`session.gc_probability`: https://www.php.net/manual/en/session.configuration.php#ini.session.gc-probability
.. _`session.gc_divisor`: https://www.php.net/manual/en/session.configuration.php#ini.session.gc-divisor
.. _`session_gc()`: https://www.php.net/session_gc
