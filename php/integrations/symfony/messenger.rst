Symfony Messenger [language: PHP]
=================================

Symfony `Messenger <https://symfony.com/doc/current/components/messenger.html>`_
helps applications send and receive messages.
Integrating Blackfire with Symfony Messenger lets you **monitor** your
Message Handlers and track individual message processing.

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

.. _symfony-messenger-automatic-monitoring:

Automatic monitoring
--------------------

.. note::

    Automatic monitoring of Messenger workers is in beta and opt-in.

The **Probe** monitors your ``messenger:consume`` workers with a single
setting, without any middleware or code change:

.. code-block:: ini

    blackfire.apm_cli_workers = 1

You can also use an environment variable:

.. code-block:: bash

    $ BLACKFIRE_APM_CLI_WORKERS=1 php bin/console messenger:consume async

Requirements
~~~~~~~~~~~~

* Blackfire PHP Probe 2026.10.1 or later;
* PHP 8.2 or later, with ``blackfire.observer_api`` enabled (the default);
* the ``cli`` SAPI;
* no Suhosin or Snuffleupagus extension, as both lock the Probe.

When a worker runs on the ``cli`` SAPI but another requirement is missing, the
Probe ignores the setting and logs a message at the info level. Set
``blackfire.log_level`` to ``3`` or higher to see it.

What Blackfire monitors
~~~~~~~~~~~~~~~~~~~~~~~

* Blackfire creates one transaction per message, named after the message
  class.
* Wrapper messages take the name of the work they carry: ``RedispatchMessage``
  uses the name of the wrapped message, ``RunCommandMessage`` the command name,
  and a Scheduler ``ServiceCallMessage`` the service and method
  (``@service::method``). Each scheduled task gets its own name.
* Blackfire creates one transaction per batch handler flush, named after the
  handler class.
* Blackfire measures peak memory per message, not for the whole worker process.
* Blackfire samples messages like web requests and counts failed messages as
  errors.

.. tip::

    You can keep the setting enabled for all CLI commands. Commands that do not
    run a Messenger worker are not affected and do not contact the **Agent**.

.. _symfony-messenger-concurrent-workers:

Concurrent workers
~~~~~~~~~~~~~~~~~~

Symfony Messenger 8.2+ handles messages in parallel with the ``--concurrency``
option:

.. code-block:: bash

    $ php bin/console messenger:consume async --concurrency=4

The parent process dispatches messages to its children and sends no
transaction. Each child sends one transaction per message it handles.

Monitoring concurrent workers requires Blackfire PHP Probe 2026.10.3 or later
and PHP 8.4 or later, which Symfony Messenger 8.2 also requires.

.. caution::

    By default, children run as separate PHP processes and do not inherit
    ``php -d`` options. The following command monitors nothing:

    .. code-block:: bash

        $ php -d blackfire.apm_cli_workers=1 bin/console messenger:consume async --concurrency=4

    Enable the setting in ``php.ini`` or with the ``BLACKFIRE_APM_CLI_WORKERS=1``
    environment variable instead. Children started as ``ext-parallel`` threads
    inherit ``-d`` options.

Limitations
~~~~~~~~~~~

* Blackfire does not monitor workers started with FrankenPHP ``php-cli``.
* When a handler starts an external program, such as ffmpeg or Ghostscript,
  Blackfire measures the time spent waiting for it, but not its memory and CPU
  usage.

To report a gap during the beta, `open a ticket on the Blackfire support site <https://support.blackfire.upsun.com>`_.

.. _symfony-messenger-migrating-from-sdk:

Migrating from the SDK middleware
---------------------------------

If you monitor your workers with the ``MonitoredMiddleware``, automatic
monitoring replaces it with a single setting instead of one middleware per bus.
Keep the middleware if your workers run PHP 8.1 or earlier.

1. Upgrade the Blackfire PHP Probe to 2026.10.1 or later, or 2026.10.3 or later
   for :ref:`concurrent workers <symfony-messenger-concurrent-workers>`.

2. Enable ``blackfire.apm_cli_workers`` on your workers:

   .. code-block:: ini

       blackfire.apm_cli_workers = 1

3. Deploy. You can keep the middleware during the rollout: Blackfire still
   creates one transaction per message, not two.

4. Remove the middleware from every bus, and remove its service definition:

   .. code-block:: diff

        framework:
          messenger:
            buses:
              messenger.bus.default:
                middleware:
       -          - 'Blackfire\Bridge\Symfony\MonitoredMiddleware'

       -services:
       -  Blackfire\Bridge\Symfony\MonitoredMiddleware: ~

5. Remove the ``blackfire/php-sdk`` dependency if nothing else in your project
   uses it.

What changes on your dashboards
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Blackfire monitors every bus, including buses where you never added the
  middleware.
* ``RedispatchMessage``, ``RunCommandMessage`` and Scheduler
  ``ServiceCallMessage`` transactions take the name of the work they carry.
  Update the filters that rely on the old names.
* Durations increase slightly, because a transaction covers the whole message
  handling, including worker event listeners and every middleware, not only
  what runs after the Blackfire middleware.
* Memory values drop, because Blackfire measures peak memory per message
  instead of for the whole worker process.
* Batch handler flushes appear as separate transactions.

Monitoring with the SDK
-----------------------

.. tip::

    On PHP 8.2 or later, :ref:`automatic monitoring <symfony-messenger-automatic-monitoring>`
    needs no middleware. See :ref:`symfony-messenger-migrating-from-sdk`.

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.27+ version).

The Blackfire PHP SDK provides a **Symfony Messenger middleware** that eases
collecting and measuring the processing of your messages:

.. code-block:: yaml
    :emphasize-lines: 6,9

    framework:
      messenger:
        buses:
          messenger.bus.default:
            middleware:
              - 'Blackfire\Bridge\Symfony\MonitoredMiddleware'

    services:
      Blackfire\Bridge\Symfony\MonitoredMiddleware: ~

A transaction name is generated for every processed message given the class name
of the message. It allows monitoring of consumers given message types.

Transactions are visible on the Monitoring dashboard page, filtering on ``CLI``
requests.
