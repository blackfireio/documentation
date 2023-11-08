"session.use_only_cookies" should be enabled
============================================

When the `session.use_only_cookies`_ ini setting is enabled, PHP session module
only accepts session ids from cookies. This setting prevents attacks passing the
session id in the URL.

It's therefore highly recommended to enable this setting using
``session.use_only_cookies=On`` (or remove the setting since its default value
is ``On``).

.. _`session.use_only_cookies`: https://www.php.net/manual/en/session.configuration.php#ini.session.use-only-cookies
