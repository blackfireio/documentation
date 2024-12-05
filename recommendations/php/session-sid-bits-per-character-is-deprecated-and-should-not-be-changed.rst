"session.sid_bits_per_character" is deprecated and should not be changed
========================================================================

The `session.sid_bits_per_character`_ ini setting allowed developers to specifies
the number of bits in encoded session ID character.

Changing the value of this settings is now deprecated in PHP 8.4.

Developers should update the session storage backend to accept 32 character
hexadecimal session IDs and stop changing these two INI settings instead.

.. _`session.sid_bits_per_character`: https://www.php.net/manual/en/session.configuration.php#ini.session.sid-bits-per-character
