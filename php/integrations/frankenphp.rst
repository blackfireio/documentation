FrankenPHP [language: PHP][status: beta]
========================================

.. caution::

    FrankenPHP support is in beta and not yet feature-complete.

`FrankenPHP <https://frankenphp.dev/>`_ is a modern application server for PHP
built on top of the `Caddy <https://caddyserver.com/>`_ webserver

Requirements
------------

- :doc:`PHP Probe </up-and-running/update>` >= ``v1.92.44``

Coverage
--------

- :doc:`Deterministic Profiling </monitoring-cookbooks/index>`: Fully supported.
  Some code changes may be required (:ref:`see below <frankenphp-profiling>`).
- :doc:`Monitoring </monitoring-cookbooks/index>`: Supported, without Automatic Profiling.
- :doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`: Supported
  via the Datadog extension on ZTS builds.
- :doc:`Browser Monitoring </front-end-observability/browser-monitoring>`: Fully supported

Manual Installation
-------------------

FrankenPHP requires a ZTS (Zend Thread Safety) build of the Blackfire PHP Probe,
which you can install by following our :doc:`installation guides </up-and-running/installation>`.

Docker
------

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

.. _frankenphp-profiling:

Deterministic Profiling
-----------------------

.. note::

    **Laravel Octane users**: :doc:`our integration </php/integrations/laravel/octane>`
    supports Deterministic Profiling out of the box.

If you are not using Laravel Octane, update your FrankenPHP worker script to
control the instrumentation manually:

.. code-block:: php

    <?php

    ignore_user_abort(true);

    $handler = static function () {
        echo 'Hello Blackfire!';
    };

    $blackfireMiddleware = static function () use ($handler) {
        $probe = null;
        // Only create a Blackfire probe if the Blackfire header is present
        if (isset($_SERVER['HTTP_X_BLACKFIRE_QUERY'])) {
            $probe = new \BlackfireProbe($_SERVER['HTTP_X_BLACKFIRE_QUERY']);
            $probe->enable();
        }

        try {
            $handler();
        } catch (\Throwable $e) {
            throw $e;
        } finally {
            if (probe) {
                $probe->close();
            }
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

Monitoring
----------

Monitoring requires :doc:`PHP Probe </up-and-running/update>` ``v1.92.44`` or later.

:doc:`Automatic profiling </monitoring-cookbooks/automatic-profiling>` isn't
supported yet.


Report an issue
---------------

FrankenPHP support is still in beta.
If you run into a problem, please `open a ticket on the Blackfire support site <https://support.blackfire.io>`_.
