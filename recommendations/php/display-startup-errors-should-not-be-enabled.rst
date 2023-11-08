"display_startup_errors" should not be enabled
==============================================

The `display_startup_errors`_ ini setting, when enabled, displays the full
contents of the PHP startup sequence's errors in the web page (for web
applications) or the command console output (for scripts and commands).

These errors are generally related to PHP extensions and some of them may leak
sensitive information or even prevent sending HTTP headers.

Displaying these messages is useful in development to debug configuration issues.
However, displaying them in production is a bad practice you should avoid.

It's strongly recommended to disable this setting in your ``php.ini``
configuration using ``display_startup_errors=off``.

.. _`display_startup_errors`: https://www.php.net/manual/en/errorfunc.configuration.php#ini.display-startup-errors
