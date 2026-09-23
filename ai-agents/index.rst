AI agents
=========

Making sense of observability data can be cumbersome. AI coding agents can be
effective at assisting you, provided some configuration.

Install the agent-facing components in a project where Blackfire already runs:
the :doc:`MCP server <mcp-server>`, the :doc:`skills <skills>`, or both.

Requirements
------------

- :ref:`Blackfire Agent <installation-instructions>` >= ``v2026.9.1``

AI components
-------------

The MCP server and skills cover different needs, and work together:

- the :doc:`MCP server <mcp-server>` provides the tools: what CLI commands are
  available? What are their signatures and purpose?
- the :doc:`skills <skills>` provide the method: which command answers which
  question.

.. note::

    Blackfire AI support is in beta. Current support covers :doc:`deterministic profiling </profiling-cookbooks/index>`.

    The scope of the MCP server, skills, and the CLI grows with each iteration.

.. toctree::
    :maxdepth: 2
    :titlesonly:

    MCP Server <mcp-server>
    Skills <skills>
