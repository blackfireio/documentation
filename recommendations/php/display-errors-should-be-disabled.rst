"display_errors" should be disabled
===================================

The `display_errors`_ ini setting, when enabled, displays the full contents of
the PHP errors in the web page (for web applications) or the command console
output (for scripts and commands).

Some error messages can leak sensitive information, such as PDO exceptions that
include the database credentials, whereas some others prevent sending HTTP
headers and cause issues in your web applications.

Displaying errors this way is a bad practice you should avoid. Use the
`log_errors`_ setting instead if you want to collect these errors.

It's strongly recommended to disable this setting in your ``php.ini``
configuration using ``display_errors=off``.

.. _`display_errors`: https://www.php.net/manual/en/errorfunc.configuration.php#ini.display-errors
.. _`log_errors`: https://www.php.net/manual/en/errorfunc.configuration.php#ini.log-errors
