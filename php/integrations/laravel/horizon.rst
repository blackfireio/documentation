Laravel Horizon and queue services [language: PHP]
==================================================

Laravel `Horizon <https://laravel.com/docs/horizon>`_ supercharges the Laravel
powered Redis queues.

Integrating Blackfire with Laravel queue services lets you **monitor** your
consumers and track individual job processing, either automatically with the
**Probe** or with the Blackfire PHP SDK.

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

.. _laravel-queue-automatic-monitoring:

Automatic monitoring
--------------------

.. note::

    Automatic monitoring of Laravel queue workers is in beta and opt-in.

The **Probe** monitors your ``queue:work`` and Horizon workers with a single
setting, without any service provider or code change:

.. code-block:: ini

    blackfire.apm_cli_workers = 1

You can also use an environment variable:

.. code-block:: bash

    $ BLACKFIRE_APM_CLI_WORKERS=1 php artisan queue:work

Requirements
~~~~~~~~~~~~

* Blackfire PHP Probe ``>= 2026.11.0``;
* PHP 8.2 or later, with ``blackfire.observer_api`` enabled (the default);
* no Suhosin or Snuffleupagus extension, as both lock the Probe.

When a worker runs on the ``cli`` SAPI but another requirement is missing, the
Probe ignores the setting and logs a message at the info level. Set
``blackfire.log_level`` to ``3`` or higher to see it.

What Blackfire monitors
~~~~~~~~~~~~~~~~~~~~~~~

* Blackfire creates one transaction per job, for workers started with
  ``queue:work``, ``queue:work --once``, ``queue:listen`` and ``horizon``.
* Each transaction takes the job display name: the job class, or the class of
  the queued event listener, mailable or notification it carries. A queued
  closure is named after its file and line, like ``Closure (web.php:12)``.
* Blackfire measures peak memory per job, not for the whole worker process.
* Blackfire samples jobs like web requests. Monitoring does not report errors
  for CLI transactions, so a job that throws an exception or calls
  ``$this->fail()`` appears like a successful one.
* When a job exceeds its timeout, Blackfire sends its transaction before the
  worker kills the process. Job timeouts require the ``pcntl`` extension, as in
  Laravel.
* A job that the ``Skip`` middleware deletes never runs, so it creates no
  transaction. A job released back to the queue, for instance by the
  ``RateLimited`` middleware, gets a new transaction each time a worker runs it.

.. tip::

    You can keep the setting enabled for all CLI commands. Commands that do not
    run a queue worker are not affected and do not contact the **Agent**.

.. caution::

    ``queue:listen`` and ``horizon`` run jobs in child PHP processes, which do
    not inherit ``php -d`` options. The following command monitors nothing:

    .. code-block:: bash

        $ php -d blackfire.apm_cli_workers=1 artisan horizon

    Enable the setting in ``php.ini`` or with the ``BLACKFIRE_APM_CLI_WORKERS=1``
    environment variable instead.

Limitations
~~~~~~~~~~~

* Blackfire does not monitor workers started with FrankenPHP ``php-cli``.
* Jobs dispatched to the ``sync``, ``deferred`` or ``background`` connections
  run without a queue worker, so they do not get their own transaction.
* Blackfire does not monitor a custom worker class that overrides
  ``Illuminate\Queue\Worker::process()`` without calling the parent method.

To report a gap during the beta, `open a ticket on the Blackfire support site <https://support.blackfire.upsun.com>`_.

.. _laravel-queue-migrating-from-sdk:

Migrating from the SDK service provider
---------------------------------------

If you monitor your workers with the ``ObservableJobProvider``, automatic
monitoring replaces it with a single setting. Keep the service provider if your
workers run PHP 8.1 or earlier.

1. Upgrade the Blackfire PHP Probe to ``2026.11.0`` or later.

2. Enable ``blackfire.apm_cli_workers`` on your workers:

   .. code-block:: ini

       blackfire.apm_cli_workers = 1

3. Deploy. You can keep the service provider during the rollout: Blackfire
   still creates one transaction per job, not two.

4. Remove ``Blackfire\Bridge\Laravel\ObservableJobProvider`` from your service
   providers.

Monitoring with the SDK
-----------------------

Requirements
~~~~~~~~~~~~

- PHP >= 7.3
- ``illuminate/queue`` >= 8.0
- ``illuminate/support`` >= 8.0

Installation
~~~~~~~~~~~~

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.27+ version).

Configuration
~~~~~~~~~~~~~

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
