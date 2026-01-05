Symfony Runtime [language: PHP][status: beta]
=============================================

.. caution::

    Symfony Runtime support is in beta and not yet feature-complete.

The `Symfony Runtime Component <https://symfony.com/packages/Runtime>`_ application bootstrapping from the execution environment, allowing the same code to run on traditional servers (PHP-FPM) or high-performance, long-running runtimes (:doc:`FrankenPHP </php/integrations/frankenphp>`, :doc:`FrankenPHP </php/integrations/swoole>`, ReactPHP...) without modification.

Requirements
------------

- :doc:`PHP Probe </up-and-running/update>` >= ``v1.92.44``
- :doc:`Our FrankenPHP integration </php/integrations/frankenphp>` is required.

FrankenPHP Integration
----------------------

`FrankenPHP <https://frankenphp.dev/>`_ is a modern PHP application server built on Caddy webserver. Blackfire probe support for FrankenPHP is in **beta status**.

Installation
~~~~~~~~~~~~

1. Add :ref:`Blackfire PHP SDK v2.51.0+ <php-sdk-installation>` as a dependency
2. Register the profiler subscriber using the Symfony ``config/services.yaml`` file:

.. code-block:: yaml

    services:
        Blackfire\Bridge\Symfony\EventSubscriber\FrankenPHPProfilerSubscriber:
            tags:
                - { name: kernel.event_subscriber }

Report an issue
---------------

Symfony Runtime support is still in beta.
If you run into a problem, please `open a ticket on the Blackfire support site <https://support.blackfire.io>`_.
