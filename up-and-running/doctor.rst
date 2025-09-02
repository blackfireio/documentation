Blackfire Doctor
================

.. include-twig:: `youtube-iframe`
    :title: Blackfire Doctor
    :src: https://www.youtube-nocookie.com/embed/OXU1YJJwCXM?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

The ``blackfire doctor`` CLI command is the go-to tool to validate your Blackfire installation. It automatically checks your :doc:`Agent <configuration/agent>`,
:term:`Probe <Probe>`, configuration, and connectivity.

``blackfire doctor`` provides:

- Instant confirmation your setup is correct.
- Guidance when something's off.
- A clear human-readable report you can share with `our support team <https://support.blackfire.platform.sh/>`_ if you need extra help.

Requirements
------------

- :doc:`Blackfire Agent <configuration/agent>` >= 2.29.0

Usage
-----

.. code-block:: bash

    blackfire doctor

Troubleshoot Remote Installation
--------------------------------

``blackfire doctor`` can help troubleshoot remote installations by passing the
``--socket`` option.

.. warning::

    While remote troubleshooting is supported, **never expose the Blackfire
    Agent publicly**. You are fully responsible for securing your agent enabling
    remote access.

.. code-block:: bash

    blackfire doctor --socket /path/to/blackfire-agent.sock

Running in Docker
~~~~~~~~~~~~~~~~~~

You can use ``blackfire doctor`` on your host machine to validate a
:doc:`Docker/OCI <docker>` setup containing an Agent normally available on
port ``8307``:

.. code-block:: bash

    blackfire doctor --socket=tcp://localhost:8307
