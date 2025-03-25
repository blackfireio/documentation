.env configuration should not be parsed in production
=====================================================

On production servers, you should define real environment variables
instead of loading them from a ``.env`` file.
This will prevent your app from consuming resources on parsing the ``.env`` file for every HTTP request.

Since Symfony Flex 1.2, running ``composer dump-env prod`` when building your application is required.

Defining environment variables depends on the web server and/or hosting provider you are using.
If you are using Symfony, please read the `dedicated documentation`_.

.. _`dedicated documentation`: https://symfony.com/doc/current/configuration.html#configuring-environment-variables-in-production