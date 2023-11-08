OPcache interned strings buffer should not use more than 85% of its allocated memory
====================================================================================

Interned strings are a nice memory optimization that was added in PHP 5.4.
PHP stores immutable strings (a ``char *``) into a special buffer to be able
to reuse its pointer for all occurrences of the same string.

Blackfire recommends that the interned strings buffer does not represent more than 85% of the allocated memory.

This `setting`_ can be adjusted using the ``opcache.interned_strings_buffer``.
You can also read this article about `PHP string management`_ and
this article dedicated to `OPcache`_

.. _`setting`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.interned-strings-buffer
.. _`OPcache`: http://blog.jpauli.tech/2015-03-05-opcache-html/#sharinginternedstrings
.. _`PHP string management`: http://blog.jpauli.tech/2015-09-18-php-string-management-html/#internedstrings
