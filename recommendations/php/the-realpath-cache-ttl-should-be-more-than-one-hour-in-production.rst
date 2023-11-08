The realpath cache ttl should be more than one hour in production
=================================================================

The `realpath()`_ function returns the absolute path for any given relative
file path. This conversion takes a non-negligible time because it performs some
filesystem calls. That's why PHP caches the results of ``realpath()`` calls
and their associated `stat()`_ calls.

The realpath information is only cached for file paths that exist and is used
for most of the PHP filesystem calls. Complex applications involve a lot of file
operations, so this cache has a significant impact in your application
performance.

The `realpath_cache_ttl`_ ini setting controls the time in seconds for which the
realpath information is cached for a given file or directory. In production,
files are not supposed to be updated, so you must increase this cache time at
least to one hour using ``realpath_cache_ttl=3600``.

.. _`realpath()`: https://www.php.net/manual/en/function.realpath.php
.. _`realpath_cache_ttl`: https://www.php.net/manual/en/ini.core.php#ini.realpath-cache-ttl
.. _`stat()`: https://www.php.net/manual/en/function.stat.php
