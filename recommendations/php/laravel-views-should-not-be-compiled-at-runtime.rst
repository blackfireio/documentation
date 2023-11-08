Laravel Views Should Not Be Compiled at Runtime
===============================================

To avoid unnecessary computations in production, **Laravel compiles Blade template
views**.

By default, Blade template views are compiled on demand as Laravel determines if
the requested view has a compiled version and that it is not stale.
When applicable, Laravel compiles the views on-the-fly, which can add a negative
impact on performance. However, in production, the views are not expected to change.

Laravel provides an Artisan command in order to pre-compile your application views:

.. code-block:: bash

    $ php artisan view:cache

This command will generate multiple PHP files in `storage/framework/views/` directory,
compiled off the Blade templates used in your application.
Make sure those files are present on your server in order to benefit from this
cache.

It is advised to run this command as part of your deployment process.

Read the `Laravel view documentation`_ for further information.

.. _`Laravel view documentation`: https://laravel.com/docs/8.x/views#optimizing-views
