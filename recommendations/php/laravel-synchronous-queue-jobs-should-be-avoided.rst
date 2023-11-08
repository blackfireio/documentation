Laravel synchronous queue jobs should be avoided
================================================

`Laravel Queues`_ are designed to delegate heavy tasks to background jobs to
avoid performing these tasks during a web request.

While queued jobs are generally processed asynchronously, using dedicated queue
backends (e.g., Redis, Beanstalkd, Amazon SQS...), `one may trigger them
synchronously`_, during the current process.

**Synchronous jobs are usually bad for performance as heavy tasks slow down the
current web request**.

Therefore, using the ``dispatchSync()`` method from a job class is highly
discouraged.

.. _`Laravel Queues`: https://laravel.com/docs/8.x/queues

.. _`one may trigger them synchronously`: https://laravel.com/docs/8.x/queues#synchronous-dispatching
