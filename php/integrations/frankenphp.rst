FrankenPHP [language: PHP]
==========================

`FrankenPHP <https://frankenphp.dev/>`_ is a modern application server for PHP
built on top of the `Caddy <https://caddyserver.com/>`_ webserver

Requirements
------------

- :doc:`PHP Probe </up-and-running/update>` >= ``v2026.10.4``

Coverage
--------

- :doc:`Deterministic Profiling </profiling-cookbooks/index>`: Fully supported.
- :doc:`Monitoring </monitoring-cookbooks/index>`: Supported, with Automatic Profiling.
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

Support
-------

`Watching for files mode <https://frankenphp.dev/docs/config/#watching-for-file-changes>`_ isn't supported yet.

`Hot Reloading <https://frankenphp.dev/docs/hot-reload/>`_ isn't supported yet.
