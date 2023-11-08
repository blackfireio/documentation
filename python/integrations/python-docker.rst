Python Probe with Docker [language: Python]
===========================================

Enabling the Python Probe
-------------------------

To be able to use Blackfire, add the probe to your Docker PHP image. Here is an
example of a ``Dockerfile`` based on the official Docker Python image:

.. code-block:: bash

    FROM python:3.9-buster

    RUN pip install --upgrade pip blackfire

.. note:: 

    **Base image**

    This example targets official Python Docker images. If you are using a
    custom image, you probably need to adapt it.

Build your container as usual:

.. code-block:: bash
    :zerocopy:

    docker build -t python-blackfire .

.. note:: 

    **Upgrading**

    To upgrade the Probe, rebuild your Python container and relaunch it (you
    might need to use the ``--no-cache`` option to force the download of the
    latest Probe version).

Docker Compose
~~~~~~~~~~~~~~

If you use ``docker compose``, you can connect your ``Python`` container and the
agent using the following snippet:

:include_twig:`docker_compose_context`

Using the Client for CLI Profiling
-----------------------------------

When profiling command line scripts, :ref:`the process is slightly different
than for HTTP requests <docker-http-profiling>`.

You execute ``blackfire run`` which in the end runs an embedded agent and
wraps your Python script with the required environment variables. Therefore, in
this configuration you do not need to (and cannot) use the
``blackfire/blackfire`` image.

Instead, you need to fetch and use the ``blackfire`` client binary inside your
Python container.

Installing Blackfire Client
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here is an example of a ``Dockerfile`` based on the official Docker Python image
that retrieves the client at build time:

.. code-block:: text
    :zerocopy:

    FROM python:3.9-buster

    RUN pip install --upgrade pip blackfire
    RUN mkdir -p /tmp/blackfire \
        && architecture=$(uname -m) \
        && curl -A "Docker" -L https://blackfire.io/api/v1/releases/cli/linux/$architecture | tar zxp -C /tmp/blackfire \
        && mv /tmp/blackfire/blackfire /usr/bin/blackfire \
        && rm -Rf /tmp/blackfire

Build your container as usual:

.. code-block:: bash
    :zerocopy:

    docker build -t python-blackfire .

Debugging the Python Probe
--------------------------

By default, the Probe is quiet and does not produce logs. To debug issues,
pass ``-e BLACKFIRE_LOG_LEVEL=4`` to the ``docker run`` command, and tail the
logs via Docker:

.. code-block:: bash
    :zerocopy:

    docker logs -f PYTHON_CONTAINER_ID

Installing the Agent
--------------------

To install the Blackfire Agent using Docker, please refer to
:doc:`the dedicated documentation page </up-and-running/docker>`.
