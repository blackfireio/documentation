PHP Probe with Docker [language: PHP]
=====================================

Enabling the PHP Probe
----------------------

To be able to use Blackfire, add the probe to your Docker PHP image. Here is an
example of a ``Dockerfile`` based on the official Docker PHP image:

.. caution::

    Choose the snippet corresponding to the base system you are using
    (``Linux`` or ``Alpine``).

.. include-twig:: `docker_php_probe`

.. note:: 

    **Base image**

    This example targets official PHP Docker images. If you are using a custom
    image, you probably need to adapt it.

    A common mistake while adapting it for custom images is the lack of
    ``PHP_INI_DIR``. In such case you can get it by using ``php -i | grep
    "additional .ini"``.

    An alternative solution is to proceed with the regular Blackfire
    installation using the package manager available with your base image OS.

.. caution::

    If you are using a ``zts`` (`Zend Thread Safety`) version of PHP, please add
    ``-zts`` to the version name.

Build your container as usual:

.. code-block:: bash
    :zerocopy:

    docker build -t php-blackfire .

.. note:: 

    **Upgrading**

    To upgrade the Probe, rebuild your PHP container and relaunch it (you might
    need to use the ``--no-cache`` option to force the download of the latest
    Probe version).

Docker Compose
~~~~~~~~~~~~~~

If you use ``docker compose``, you can connect your ``PHP`` container and the
agent using the following snippet:

.. include-twig:: `docker_compose_context`

Using the Client for CLI Profiling
-----------------------------------

When profiling command line scripts, :ref:`the process is slightly different
than for HTTP requests <docker-http-profiling>`.
You execute ``blackfire run`` which in the end runs an embedded agent and
wraps your PHP script with the required environment variables. Therefore, in
this configuration, you do not need to (and cannot) use the
``blackfire/blackfire`` image.
Instead, you need to fetch and use the ``blackfire`` client binary inside your
PHP container.

Here is an example of a ``Dockerfile`` based on the official Docker PHP image
that retrieves the client at build time:

.. code-block:: text
    :zerocopy:

    FROM php:8.2-fpm

    RUN mkdir -p /tmp/blackfire \
        && architecture=$(uname -m) \
        && curl -A "Docker" -L https://blackfire.io/api/v1/releases/cli/linux/$architecture | tar zxp -C /tmp/blackfire \
        && mv /tmp/blackfire/blackfire /usr/bin/blackfire \
        && rm -Rf /tmp/blackfire

Build your container as usual:

.. code-block:: bash
    :zerocopy:

    docker build -t php-blackfire .

With exposed ``BLACKFIRE_CLIENT_ID`` and ``BLACKFIRE_CLIENT_TOKEN`` environment
variables, you can now directly execute ``blackfire run php myscript.php``
within your PHP container.

.. include:: ../../profiling-cookbooks/_cli-profiling-warning.rst

Debugging the PHP Probe
-----------------------

By default, the Probe is quiet and does not produce logs. To debug issues,
pass ``-e BLACKFIRE_LOG_LEVEL=4`` to the ``docker run`` command, and tail the
logs via Docker:

.. code-block:: bash
    :zerocopy:

    docker logs -f PHP_CONTAINER_ID

Installing the Agent
--------------------

To install the Blackfire Agent using Docker, please refer to
:doc:`the dedicated documentation page </up-and-running/docker>`.
