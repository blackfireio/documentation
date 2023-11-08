Laravel routes should be cached
===============================

To avoid unnecessary computations in production, Laravel uses a
**route cache**.

This cache is not enabled in development to detect dynamically route changes.
However, in production, the routes are not expected to change.

To enable the routes cache on your application, run the following:

.. code-block:: bash

    $ php artisan route:cache

This command will generate a PHP file in `bootstrap/cache/` directory. Make sure
this file is present on your server in order to benefit from this cache.

Read the `Laravel routing documentation`_ for further information.

.. _`Laravel routing documentation`: https://laravel.com/docs/8.x/routing#route-caching
