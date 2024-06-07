"opcache.validate_timestamps" should be enabled
===============================================

While it may seem counter intuitive to enable the
`opcache.validate_timestamps`_ setting, timestamp validation by OPcache gets
through PHP's realpath cache. This means that the check is usually really fast as
it doesn't hit the (slow) file system.

By enabling this setting, your PHP engine behaves in a more predictable way, and
allows enabling the `opcache.enable_file_override`_ ini setting.

.. _`opcache.validate_timestamps`: https://www.php.net/manual/opcache.configuration.php#ini.opcache.validate-timestamps
.. _`opcache.enable_file_override`: https://www.php.net/manual/opcache.configuration.php#ini.opcache.enable-file-override
