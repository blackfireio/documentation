The Blackfire MCP server
========================

Blackfire provides a local MCP (`Model Context Protocol`_) via the CLI command
``blackfire mcp``.

Registering the MCP
-------------------

Claude Code
~~~~~~~~~~~

.. code-block:: bash

    claude mcp add blackfire -- blackfire mcp

Claude Code runs everything after ``--``. Add ``--scope user`` to make the
Blackfire MCP available in all your projects, or ``--scope project`` to write it
to a ``.mcp.json`` file you commit for your team:

.. code-block:: bash

    claude mcp add --scope user blackfire -- blackfire mcp

Codex CLI
~~~~~~~~~

.. code-block:: bash

    codex mcp add blackfire -- blackfire mcp

To edit the configuration file instead, add the following to
``~/.codex/config.toml``:

.. code-block:: toml

    [mcp_servers.blackfire]
    command = "blackfire"
    args = ["mcp"]

Run ``/mcp`` in a Codex session to check that the tools are listed.

OpenCode
~~~~~~~~

Declare the server in the ``mcp`` block of ``opencode.json``, in your project
root, or in ``~/.config/opencode/opencode.json`` for every project:

.. code-block:: json

    {
        "$schema": "https://opencode.ai/config.json",
        "mcp": {
            "blackfire": {
                "type": "local",
                "command": ["blackfire", "mcp"],
                "enabled": true
            }
        }
    }

Pi
~~

Pi reaches MCP servers through the ``pi-mcp-adapter`` package:

.. code-block:: bash

    pi install npm:pi-mcp-adapter

Restart Pi, then declare the server in ``~/.pi/agent/mcp.json``, or in a
``.mcp.json`` file at your project root:

.. code-block:: json

    {
        "mcpServers": {
            "blackfire": {
                "command": "blackfire",
                "args": ["mcp"]
            }
        }
    }


.. _`Model Context Protocol`: https://modelcontextprotocol.io
