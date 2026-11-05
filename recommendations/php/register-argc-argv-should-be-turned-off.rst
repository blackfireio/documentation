"register_argc_argv" should be turned off
=========================================

The `register_argc_argv`_ ini setting tells PHP whether to declare the
argv & argc variables (that would contain the GET information).
When the setting is set to ``on``, attackers can craft URL containing
values in the query string that might be interpreted as an env variable
by a framework.

The ``register_argc_argv`` setting is ``on`` by default up to PHP 8.4, and many
distributions override this value to ``off`` in their ``php.ini-production``
file. PHP 8.5 changes the default to ``off`` and deprecates deriving
``$_SERVER['argv']`` from the query string. It's strongly recommended to disable
it in your ``php.ini`` configuration using ``register_argc_argv=off``.

Blackfire only checks this setting on HTTP requests, as the PHP CLI always
declares the argv & argc variables.

.. _`register_argc_argv`: https://www.php.net/manual/en/ini.core.php#ini.register-argc-argv
