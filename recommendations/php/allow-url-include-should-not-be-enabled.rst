"allow_url_include" should not be enabled
=========================================

The `allow_url_include`_ ini setting allows running PHP scripts hosted on a remote server
using the ``include``, ``include_once()``, ``require()`` or ``require_once()`` functions.

A malicious user could make PHP include or require scripts stored in external
services and compromise your own servers.

It's strongly recommended to disable this setting in your ``php.ini``
configuration using ``allow_url_include=off``.

.. _`allow_url_include`: https://www.php.net/manual/en/filesystem.configuration.php#ini.allow-url-include
