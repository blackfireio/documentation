"track_errors" should not be enabled
====================================

When the `track_errors`_ ini setting is enabled, a ``$php_errormsg`` variable is
created in the local scope whenever a non-fatal error is thrown and is not
processed by an error handler.

Relying on this ``$php_errormsg`` variable is risky and makes the application
non-portable: if you deploy the application into a server that has the
``track_errors`` ini setting disabled, the application will stop working.

The ``error_get_last()`` function provides a cleaner way of retrieving the last
error. Moreover, PHP 7 added a new ``error_clear_last()`` function to solve the
last possible use-case of the ``track_errors`` setting.

For these reasons, the ``track_errors`` setting `has been deprecated in PHP
7.2`_ and it's strongly recommended to disable it in your ``php.ini``
configuration using ``track_errors=off`` (or by removing it, since "off" is the
default).

.. _`has been deprecated in PHP 7.2`: https://wiki.php.net/rfc/deprecations_php_7_2
.. _`track_errors`: https://www.php.net/manual/en/errorfunc.configuration.php#ini.track-errors
