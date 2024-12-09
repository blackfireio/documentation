"register_argc_argv" should be turned off
=========================================

The `register_argc_argv`_ ini setting tells PHP whether to declare the
argv & argc variables (that would contain the GET information).
When the setting is set to ``on``, attackers can craft URL containing
values in the query string that might be interpreted as an env variable
by a framework.

The ``register_argc_argv`` setting is set to ``on`` by default.
Many distribution overrides this value to ``off`` in their ``production.ini``
file. It's strongly recommended to disable it in your
``php.ini`` configuration using ``register_argc_argv=off``.

.. _`register_argc_argv`: https://www.php.net/manual/en/ini.core.php#ini.register-argc-argv
