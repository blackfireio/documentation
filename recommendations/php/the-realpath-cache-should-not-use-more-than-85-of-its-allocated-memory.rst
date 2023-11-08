The realpath cache should not use more than 85% of its allocated memory
=======================================================================

The `realpath()`_ function returns the absolute path for any given relative
file path. This conversion takes a non-negligible time because it performs some
filesystem calls. That's why PHP caches the results of ``realpath()`` calls
and their associated `stat()`_ calls. The `realpath_cache_size`_ ini setting
defines the size of this cache.

The realpath cache is only used for file paths that exist and is used for most
of PHP filesystem calls. Complex applications involve a lot of file operations,
so this cache size must be increased accordingly.

It's recommended to increase the realpath cache size gradually as much as needed
and monitor it continuously to avoid using more than 85% of its total size.

.. _`realpath()`: https://www.php.net/manual/en/function.realpath.php
.. _`realpath_cache_size`: https://www.php.net/manual/en/ini.core.php#ini.realpath-cache-size
.. _`stat()`: https://www.php.net/manual/en/function.stat.php
