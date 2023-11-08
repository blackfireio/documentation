Laravel in-memory cache should be avoided
=========================================

`Laravel Cache`_ provides an expressive, unified API for various cache backends,
including Memcached, Redis, or DynamoDB.

These backends are called "data stores" and are configured in your
``config/cache.php``. In this file, you may specify and configure the cache drivers
you may use within your application.

The special ``array`` cache driver provides an "in-memory" cache store, and can
be used in particular cases such as testing.

However, this driver only manages cache within the memory of the current process.
While storing data in memory may be helpful in some cases, the data is volatile
and is lost when the PHP process ends.

Therefore, **the "array" cache driver should be avoided in production**.

.. _`Laravel Cache`: https://laravel.com/docs/8.x/cache
