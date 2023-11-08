Laravel Artisan [language: PHP]
===============================

Laravel `Artisan <https://laravel.com/docs/artisan>`_ is the CLI command
included with Laravel.

Integrating Blackfire with Laravel Artisan lets you **monitor** all your
CLI commands:

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

Requirements
------------

- PHP >= 7.3
- ``illuminate/console`` >= 8.0
- ``illuminate/support`` >= 8.0

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in your
project (1.27+ version).

Monitoring
----------

The Blackfire PHP SDK provides a **Laravel Observable Artisan Service Provider**
that eases collecting and measuring the processing of your CLI commands.

All Laravel's `service providers <https://laravel.com/docs/providers>`_ are
registered in the ``config/app.php`` configuration file:

.. code-block:: php
    :emphasize-lines: 4

    'providers' => [
        // Other Service Providers

        Blackfire\Bridge\Laravel\ObservableCommandProvider::class,
    ],

A transaction name is generated for every processed message given the Artisan
command signature.

Transactions are visible on the Monitoring dashboard page, filtering on ``CLI``
requests.
