"expose_php" should be disabled
===============================

The `expose_php`_ ini setting exposes the PHP version used by your applications
by adding a ``X-Powered-By`` header in HTTP responses (e.g. ``X-Powered-By: PHP/7.1.3``).

This information may help malicious users because they can use the specific
vulnerabilities known for your exact PHP version.

It's strongly recommended to disable this setting in your ``php.ini``
configuration using ``expose_php=off``.

.. _`expose_php`: https://www.php.net/manual/en/ini.core.php#ini.expose-php
