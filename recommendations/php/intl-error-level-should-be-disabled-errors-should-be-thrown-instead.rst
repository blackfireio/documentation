"intl.error_level" should be disabled, errors should be thrown instead
======================================================================

The `intl.error_level`_ ini setting controls the level of error messages generated
when an error occurs in any of the `internationalization functions`_. Its value
can be any of the `error handling predefined constants`_  defined by PHP, so you
can set it to ``0`` to avoid displaying these messages.

These errors should never be displayed to the end users but handled properly.
It's better to detect the internationalization errors and throw the appropriate
exceptions instead. `Exceptions`_ are explicit, can be caught, and carry enough
information to help debugging.

Consider using the `set of functions`_ provided by the internationalization
extension to detect errors, such as ``intl_get_error_code()``.

.. _`intl.error_level`: https://www.php.net/manual/en/intl.configuration.php#ini.intl.error-level
.. _`internationalization functions`: https://www.php.net/manual/en/book.intl.php
.. _`error handling predefined constants`: https://www.php.net/manual/en/errorfunc.constants.php
.. _`Exceptions`: https://www.php.net/manual/en/language.exceptions.php
.. _`set of functions`: https://www.php.net/manual/en/ref.intl.php
