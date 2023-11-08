"user_ini.cache_ttl" should be large enough to avoid costly re-reads
====================================================================

The `user_ini.cache_ttl`_ ini setting controls the time in seconds for which the
``.user.ini`` configuration files is cached for a given file. In production,
files are not supposed to be updated, so you must increase this cache time at
least to five minutes using ``user_ini.cache_ttl=300``.

If you do not use this feature, you can also disable it using
``user_ini.filename=``.

.. _`user_ini.cache_ttl`: https://www.php.net/manual/en/configuration.file.per-user.php
