Docker
======

If you are using `Docker <https://docker.com/>`_, you might want to use the
official Blackfire Docker image to run the Agent and get some inspiration
from our recipes to install the Client and the Probe.

To ease the process of using Blackfire with Docker, define these environment
variables on the Docker **host** machine:

:include_twig:`docker_credentials`

From now on, we assume that these environment variables are set up properly.

Docker Compose
--------------

If you use ``docker compose``, you can declare the Blackfire agent as a service.
To do so, use the following snippet:

:include_twig:`docker_compose`

.. _docker-http-profiling:

CLI Client for HTTP Profiling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When profiling remote servers, you may use the Blackfire CLI tool which is
embedded in `Blackfire Docker image
<https://hub.docker.com/r/blackfire/blackfire>`_.

Assuming you configured ``blackfire`` service as explained above, you may use
the following command:

.. code-block:: bash
    :zerocopy:

    docker compose exec blackfire blackfire curl http://example.com

To make it less verbose, create an alias:

.. code-block:: bash
    :zerocopy:

    alias blackfire-curl='docker compose exec blackfire blackfire curl'
    blackfire-curl http://example.com/

.. note::

    **STDOUT & STDERR using docker compose**

    When using ``docker compose exec`` ``STDOUT`` and ``STDERR``
    outputs are mixed up. This is due to the limitations of the pseudo TTY
    which is allocated by default by Docker Compose.

    This can be an issue when using the ``--json`` option to dump a profile
    data in JSON. The profile data is indeed output to ``STDOUT`` by
    ``blackfire curl`` command, while the process info is output to ``STDERR``.

    The workaround in this case is to use Docker Compose ``-T`` option:

    .. code-block:: bash

        docker compose exec -T blackfire blackfire curl http://example.com

Debugging the Agent
~~~~~~~~~~~~~~~~~~~

By default, the agent is quiet and does not produce logs. To debug problems,
increase the log verbosity by setting ``BLACKFIRE_LOG_LEVEL`` to ``4``:

:include_twig:`docker_compose_level4`

You may then tail the logs with ``docker compose``:

.. code-block:: bash
    :zerocopy:

    docker compose logs -f blackfire

Raw Docker Image
----------------

The `Blackfire image <https://hub.docker.com/r/blackfire/blackfire>`_ is the
fastest way to get the Blackfire agent running:

.. code-block:: bash
    :zerocopy:

    docker run --name="blackfire" -d -e BLACKFIRE_SERVER_ID -e BLACKFIRE_SERVER_TOKEN blackfire/blackfire:2

.. note:: 

    **Upgrading**

    To upgrade the Blackfire image, pull the newest image from Docker and
    restart the agent container:

    .. code-block:: bash
        :zerocopy:

        docker pull blackfire/blackfire:2

    You can check the version of a running Blackfire container with the
    following command:

    .. code-block:: bash
        :zerocopy:

        docker exec blackfire blackfire-agent -v

CLI Client for HTTP Profiling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When profiling remote servers, you may use the Blackfire CLI tool which is
embedded in `Blackfire Docker image
<https://hub.docker.com/r/blackfire/blackfire>`_:

.. code-block:: bash

    docker run -it --rm \
        -e BLACKFIRE_CLIENT_ID \
        -e BLACKFIRE_CLIENT_TOKEN \
        --expose 8307 \
        blackfire/blackfire:2 blackfire \
        curl http://example.com/

To make it less verbose, create an alias:

.. code-block:: bash
    :zerocopy:

    alias blackfire-curl='docker run -it --rm -e BLACKFIRE_CLIENT_ID -e BLACKFIRE_CLIENT_TOKEN blackfire/blackfire:2 blackfire curl'
    blackfire-curl http://example.com/

.. _docker-using-probe:

Using the Probe
---------------

To install the Blackfire Probe in your application container, read the
following guides, depending on your runtime:

-   :doc:`PHP Probe with Docker </php/integrations/php-docker>`
-   :doc:`Python Probe with Docker </python/integrations/python-docker>`

Using Blackfire Player With Docker
----------------------------------

To use Blackfire Player with Docker, read the :ref:`dedicated guide <player-docker>`.
