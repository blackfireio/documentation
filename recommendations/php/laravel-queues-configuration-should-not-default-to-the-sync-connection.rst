Laravel Queues configuration should not default to the "sync" connection
========================================================================

While building a web application, you may have some tasks that take too long
to perform during a typical web request. `Laravel Queues`_ allows you to create
queued jobs that may be processed in the background.

While queued jobs are generally processed asynchronously, using dedicated queue
backends (e.g., Redis, Beanstalkd, Amazon SQS...), the ``sync`` connection may
be set as the default connection in your ``app/queue.php``.

The ``sync`` connection is **designed to handle your queued jobs synchronously**,
during the current process.

**Synchronous jobs are usually bad for performance as heavy tasks may be processed
during a web request**.

Therefore, setting the ``sync`` as the default connection
in your ``app/queue.php`` is discouraged **in favor of an asynchronous one**.

.. _`Laravel Queues`: https://laravel.com/docs/8.x/queues
