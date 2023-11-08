Laravel configuration should be cached
======================================

To avoid unnecessary computations in production, Laravel uses a
**configuration cache**.

This cache is not enabled in development to detect dynamically configuration
changes. However, in production, the configuration is not expected to change.

To enable the configuration cache on your application, run the following:

.. code-block:: bash

    $ php artisan config:cache

This command will generate multiple PHP files in `bootstrap/cache/` directory.
Make sure those files are present on your server in order to benefit from this
cache.

Read the `Laravel configuration documentation`_ for further information.

.. _`Laravel configuration documentation`: https://laravel.com/docs/8.x/configuration#configuration-caching
