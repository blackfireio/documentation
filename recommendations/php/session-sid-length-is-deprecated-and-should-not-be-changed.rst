"session.sid_length" is deprecated and should not be changed
============================================================

The `session.sid_length`_ ini setting allowed developers to specify the length
of session ID string.

Changing the value of this settings is now deprecated in PHP 8.4.

Developers should update the session storage backend to accept 32 character
hexadecimal session IDs and stop changing these two INI settings instead.

.. _`session.sid_length`: https://www.php.net/manual/en/session.configuration.php#ini.session.sid-length
