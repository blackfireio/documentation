Laravel debug mode should be disabled on production
===================================================

The `Laravel debug mode`_ determines how much information about an error is actually
displayed to the user.

This setting is set in ``config/app.php`` and follows the value of the
``APP_DEBUG`` environment variable, which is stored in your ``.env`` file.

This value should always be ``false`` in production. If not, you risk exposing
sensitive configuration values to your application's end users.

.. _`Laravel debug mode`: https://laravel.com/docs/8.x/deployment#debug-mode
