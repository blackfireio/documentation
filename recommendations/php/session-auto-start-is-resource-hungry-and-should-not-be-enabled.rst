"session.auto_start" is resource-hungry and should not be enabled
=================================================================

When the `session.auto_start`_ ini setting is enabled, the session module
starts a session automatically on request startup.

Relying on this setting makes the application
non-portable: if you deploy the application into a server that has the
``session.auto_start`` ini setting disabled, the application will stop working.

Moreover, it's common to not need sessions in some parts of web applications.
Automatically starting sessions for every URL impacts your application
performance for no real benefit.

For these reasons, it is recommended to disable it in your ``php.ini``
configuration using ``session.auto_start=off`` (or remove it, since ``off`` is
the default).

.. _`session.auto_start`: https://www.php.net/manual/en/session.configuration.php#ini.session.auto-start
