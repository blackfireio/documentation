"open_basedir" should not be set as it disables the realpath cache
==================================================================

The `open_basedir`_ ini setting limits the files PHP can open to the listed
directories. When it is set, PHP disables the `realpath cache`_ at the start of
every request, so PHP resolves the path of every included or opened file again
with system calls.

Remove ``open_basedir`` from your production configuration to keep the realpath
cache, and isolate your applications at the system level instead, with
containers or dedicated users.

.. _`open_basedir`: https://www.php.net/manual/en/ini.core.php#ini.open-basedir
.. _`realpath cache`: https://www.php.net/manual/en/ini.core.php#ini.realpath-cache-size
