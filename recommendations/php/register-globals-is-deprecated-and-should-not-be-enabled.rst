"register_globals" is deprecated and should not be enabled
==========================================================

The `register_globals`_ ini setting was used to automatically register EGPCS
(Environment, GET, POST, Cookie, Server) variables as global variables in your
applications. A `dedicated article`_ on the official PHP site explains in
detail the serious security issues that this setting may introduce.

For these reasons, the ``register_globals`` setting `was deprecated in PHP
5.3`_, removed in PHP 5.4, and it's strongly recommended to disable it in your
``php.ini`` configuration using ``register_globals=off`` (or by removing it,
since "off" is the default value).

.. _`register_globals`: https://www.php.net/manual/en/ini.core.php#ini.register-globals
.. _`dedicated article`: https://www.php.net/manual/en/security.globals.php
.. _`was deprecated in PHP 5.3`: https://www.php.net/manual/en/migration54.deprecated.php
