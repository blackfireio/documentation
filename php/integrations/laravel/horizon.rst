Laravel Horizon and queue services [language: PHP]
==================================================

Laravel `Horizon <https://laravel.com/docs/horizon>`_ supercharges the Laravel
powered Redis queues.

Integrating Blackfire with Laravel queue services lets you **monitor** your
consumers and track individual job processing:

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

Requirements
------------

- PHP >= 7.3
- ``illuminate/queue`` >= 8.0
- ``illuminate/support`` >= 8.0

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.27+ version).

Monitoring
----------

The Blackfire PHP SDK provides a **Laravel Observable Queue Service Provider**
that eases collecting and measuring the processing of your jobs.

All Laravel's `service providers <https://laravel.com/docs/providers>`_ are
registered in the ``config/app.php`` configuration file:

.. code-block:: php
    :emphasize-lines: 4

    'providers' => [
        // Other Service Providers

        Blackfire\Bridge\Laravel\ObservableJobProvider::class,
    ],

A transaction name is generated for every processed message given the class name
of the job. It allows monitoring of consumers given message types.

Transactions are visible on the Monitoring dashboard page, filtering on ``CLI``
requests.
