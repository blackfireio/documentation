"opcache.validate_timestamps" should be enabled
===============================================

While it may seem counter intuitive to enable the
`opcache.validate_timestamps`_ setting, OPcache validates the timestamp of a
cached script with a single ``stat()`` system call, at most once every
`opcache.revalidate_freq`_ seconds (2 by default). This means that the check is
usually really fast, and you can increase ``opcache.revalidate_freq`` to make it
less frequent.

By enabling this setting, your PHP engine behaves in a more predictable way, and
allows enabling the `opcache.enable_file_override`_ ini setting.

.. _`opcache.validate_timestamps`: https://www.php.net/manual/opcache.configuration.php#ini.opcache.validate-timestamps
.. _`opcache.revalidate_freq`: https://www.php.net/manual/opcache.configuration.php#ini.opcache.revalidate-freq
.. _`opcache.enable_file_override`: https://www.php.net/manual/opcache.configuration.php#ini.opcache.enable-file-override
