Symfony Messenger [language: PHP]
=================================

Symfony `Messenger <https://symfony.com/doc/current/components/messenger.html>`_
helps applications send and receive messages.
Integrating Blackfire with Symfony Messenger lets you **monitor** your
Message Handlers and track individual message processing:

.. note::

    You must, first, :doc:`enable monitoring </monitoring-cookbooks/configuration>`
    on your environment.

Installation
------------

Add :ref:`Blackfire PHP SDK <php-sdk-installation>` as a dependency in
your project (1.27+ version).

Monitoring
----------

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
