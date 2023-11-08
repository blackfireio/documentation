"session.use_strict_mode" should be enabled
===========================================

When the `session.use_strict_mode`_ ini setting is disabled, PHP session module
accepts uninitialized session ids and uses them without further validation. When
the setting is enabled, if an uninitialized session id is sent, a new session id
is generated and sent back to the browser.

Disabling this setting makes you vulnerable to `session fixation`_ attacks and
therefore, you should always enable it using ``session.use_strict_mode=On``.

.. _`session.use_strict_mode`: https://www.php.net/manual/en/session.configuration.php#ini.session.use-strict-mode
.. _`session fixation`: https://www.owasp.org/index.php/Session_fixation
