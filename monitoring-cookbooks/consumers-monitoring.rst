Consumers Monitoring
====================

.. include-twig:: `youtube-iframe`
    :title: introduction-to-blackfire
    :src: https://www.youtube-nocookie.com/embed/48uEe1dINNA?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Consumers and CLI commands can be monitored.

Displaying CLI Monitoring Data
------------------------------

The consumers and CLI command monitoring data can be displayed toggling the Web/CLI dropdown.

.. image:: ../images/monitoring/consumer_monitoring.gif

Enabling CLI Monitoring
-----------------------

Symfony Messenger workers
~~~~~~~~~~~~~~~~~~~~~~~~~

For PHP applications, a single setting monitors your Symfony Messenger workers
without any code change. Blackfire creates one transaction per consumed
message. This feature is in beta and opt-in:

.. code-block:: ini

    blackfire.apm_cli_workers = 1

See :ref:`automatic monitoring <symfony-messenger-automatic-monitoring>` for
the requirements, and :ref:`concurrent workers <symfony-messenger-concurrent-workers>`
to monitor workers started with ``--concurrency``.

Other CLI commands and consumers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You instrument other CLI commands and consumers manually:

**PHP Application**

.. code-block:: php

    // As of Blackfire PHP Probe 1.78.0
    \BlackfireProbe::startTransaction('My CLI command');

    // code

    \BlackfireProbe::stopTransaction();

**Python Application**

.. code-block:: python

    from blackfire import apm

    # As of Blackfire Python Probe 1.6.1
    apm.start_transaction()
    apm.set_transaction_name('My CLI command')

    # code

    apm.stop_transaction()

CLI transactions should be manually named either before, during, or after the
Instrumentation.

Integrations
------------

Blackfire supports a number of native integrations with third-party tools.
Please check their dedicated documentation:

* :doc:`Symfony Messenger </php/integrations/symfony/messenger>`

* :doc:`Symfony CLI commands </php/integrations/symfony/cli-commands-monitoring>`

* :doc:`Laravel Artisan </php/integrations/laravel/artisan>`

* :doc:`Laravel Horizon and queue services </php/integrations/laravel/horizon>`
