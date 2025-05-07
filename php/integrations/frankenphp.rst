FrankenPHP [language: PHP][status: beta]
========================================

.. caution::

    FrankenPHP support is currently in beta. At this stage, we only support
    deterministic profiling. Additional capabilities are in development.

`FrankenPHP <https://frankenphp.dev/>`_ is a modern application server for PHP
built on top of the `Caddy <https://caddyserver.com/>`_ webserver

Manual Installation
~~~~~~~~~~~~~~~~~~~

FrankenPHP requires a ZTS (Zend Thread Safety) build of the Blackfire PHP Probe,
which you can install by following our :doc:`installation guides </up-and-running/installation>`.

Docker
~~~~~~

Alternatively, you can use the FrankenPHP base Docker image:

.. code-block:: text
    :zerocopy:

    FROM dunglas/frankenphp

    RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION.'-zts';") \
    && architecture=$(uname -m) \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/$architecture/$version \
    && mkdir -p /tmp/blackfire \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp/blackfire \
    && mv /tmp/blackfire/blackfire-*.so $(php -r "echo ini_get ('extension_dir');")/blackfire.so \
    # blackfire.agent_socket=tcp://blackfire:8307 is only required if you're using our agent in another container.
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8307" > $PHP_INI_DIR/conf.d/blackfire.ini \
    && rm -rf /tmp/blackfire /tmp/blackfire-probe.tar.gz

Deterministic Profiling
-----------------------

.. note::

    If you're using **Laravel Octane** with FrankenPHP, :doc:`our integration </php/integrations/laravel/octane>`
    already supports Deterministic Profiling out of the box for both the classic
    and worker modes.

Classic Mode
~~~~~~~~~~~~

The Blackfire PHP probe already supports `classic mode <https://frankenphp.dev/docs/classic/>`_
without requiring additional configuration.

Worker Mode
~~~~~~~~~~~

FrankenPHP `worker mode <https://frankenphp.dev/docs/worker/>`_ requires updating
the worker script in order to control the instrumentation:

.. code-block:: php

    <?php

    ignore_user_abort(true);

    $handler = static function () {
        echo 'Hello Blackfire!';
    };

    $blackfireMiddleware = static function () use ($handler) {
        $probe = \BlackfireProbe::getMainInstance();
        $probe->enable();
        try {
            $handler();
        } catch (\Throwable $e) {
            throw $e;
        } finally {
            $probe->close();
        }
    };

    // See https://frankenphp.dev/docs/worker/ for more information
    $maxRequests = (int)($_SERVER['MAX_REQUESTS'] ?? 0);
    for ($nbRequests = 0; !$maxRequests || $nbRequests < $maxRequests; ++$nbRequests) {
        $keepRunning = \frankenphp_handle_request($blackfireMiddleware);

        gc_collect_cycles();

        if (!$keepRunning) break;
    }

Learn more about controlling Deterministic Profiling using the :ref:`PHP SDK <php-sdk-profile>`.
