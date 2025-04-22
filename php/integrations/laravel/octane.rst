Laravel Octane [language: PHP][status: beta]
============================================

Laravel `Octane <https://laravel.com/docs/octane>`_ aims at improving Laravel
applications' performance by serving them using high-powered application servers,
including :doc:`FrankenPHP </php/integrations/frankenphp>`, Swoole,
Open Swoole, and RoadRunner.

Integrating Blackfire with Laravel Octane lets you **monitor** and **profile** the
requests served through Octane:

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

Requirements
------------

- PHP >= 8.0
- ``laravel/octane`` >= 1.2.7
- ``laravel/laravel`` >= 8.81
- ``illuminate/support`` >= 8.0

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in your
project (1.30+ version).

Monitoring
----------

The Blackfire PHP SDK provides a **Laravel Octane Service Provider** that eases
collecting Monitoring data for the HTTP requests served through Octane.

All Laravel's `service providers <https://laravel.com/docs/providers>`_ are
registered in the ``config/app.php`` configuration file:

.. code-block:: php
    :emphasize-lines: 4

    'providers' => [
        // Other Service Providers

        \Blackfire\Bridge\Laravel\OctaneServiceProvider::class,
    ],

Profiling
---------

The **Laravel Octane Profiler Middleware** allows to trigger Profiles from the
:doc:`Browser Extensions</profiling-cookbooks/profiling-http-via-browser>`.

Edit your ``app/Http/Kernel.php``:

.. code-block:: php
    :emphasize-lines: 2

    protected $middleware = [
        \Blackfire\Bridge\Laravel\OctaneProfilerMiddleware::class,

        // Other Middlewares
    ];
