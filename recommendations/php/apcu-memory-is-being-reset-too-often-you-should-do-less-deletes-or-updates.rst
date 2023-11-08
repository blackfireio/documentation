APCu memory is being reset too often, you should do less deletes or updates
===========================================================================

When APCu hits its configured memory limit and cannot find any space to store
new values, it just resets its shared memory pools.

APCu keeps track of the number of times this happened. You can access this info
by reading the ``expunges`` key of the array returned by `apcu_cache_info()`_.

Expunging can happen for two reasons: either the memory limit is too small for
your use case, or the combined number of deletes and updates creates high memory
fragmentation.

Depending on your situation, you might want to increase the memory limit given to
APCu. High memory fragmentation usually means that APCu is used in a way that does
not fit its memory model, which doesn't play well with high levels of deletes and
updates (use e.g. Redis or Memcached instead.)

As things are now, users may experience bad performance and your server may
encounter high CPU usage each time the cache is expunged.

.. _`apcu_cache_info()`: https://www.php.net/apcu_cache_info
