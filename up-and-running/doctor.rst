Blackfire Doctor
================

The ``blackfire doctor`` CLI command is the go-to tool to validate your Blackfire installation. It automatically checks your :doc:`Agent <configuration/agent>`,
:term:`Probe <Probe>`, configuration, and connectivity.

``blackfire doctor`` provides:

- Instant confirmation your setup is correct.
- Guidance when something's off.
- A clear human-readable report you can share with `our support team <https://support.blackfire.platform.sh/>`_ if you need extra help.

Requirements
------------

- :doc:`Blackfire Agent </up-and-running/configuration/agent>` >= 2.29.0

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
