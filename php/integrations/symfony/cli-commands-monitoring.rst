Symfony CLI Commands Monitoring [language: PHP]
===============================================

While it is possible to :doc:`manually enable Monitoring on any CLI command
</monitoring-cookbooks/consumers-monitoring>`, we also provide an integration
allowing any Symfony commands to be traced with Blackfire Monitoring.
This is particularly useful if you run them periodically, e.g., using CRON.

.. note::

    First, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

Installation
------------

* Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
  your project (1.28+ version).

* Enable the ``MonitoredCommandSubscriber`` in your services configuration:

.. code-block:: yaml

    # config/services.yaml
    Blackfire\Bridge\Symfony\Event\MonitoredCommandSubscriber: ~

Enable Auto-Tracing
-------------------

To enable tracing on a command make it implement
``Blackfire\Bridge\Symfony\MonitorableCommandInterface``:

.. code-block:: php
    :emphasize-lines: 6

    namespace App\Command;

    use Blackfire\Bridge\Symfony\MonitorableCommandInterface;
    use Symfony\Component\Console\Command\Command;

    class MyUsefulCommand extends Command implements MonitorableCommandInterface
    {
        protected static $defaultName = 'app:useful-command';
    }

The PHP SDK provides an event subscriber that checks if the current command
has tracing enabled. A transaction name is generated for each command
based the command name. In the example above, the transaction would be named
``app:useful-command``.

Transactions are visible on the Monitoring dashboard page, filtering on ``CLI``
requests.
