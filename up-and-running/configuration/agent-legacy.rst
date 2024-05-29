Legacy Agent v1 Configuration (deprecated)
==========================================

.. warning::

  The legacy Agent v1 is deprecated and no longer maintained.

  :doc:`Upgrading to Agent v2 </up-and-running/agent-upgrade>` is required.


.. _configuration-agent-legacy:

The legacy Blackfire agent v1 can be configured via a configuration file, flags
passed to the binary, or environment variables.

Configuring the legacy Agent v1 via a Configuration File
--------------------------------------------------------

The location of the *default* agent configuration file depends on your
platform:

* On Linux: ``/etc/blackfire/agent`` (and ``/etc/default/blackfire-agent``
  :ref:`when launched as a daemon by the system <etc-default-blackfire-agent-legacy>`);

* On macOS: ``/usr/local/etc/blackfire/agent``;

* On Windows: ``C:\ProgramData\blackfire\agent.ini``.

The most important entries are ``server-id`` and ``server-token``. Here is a
typical configuration for the Agent that you can use as a template:

.. code-block:: ini

    [blackfire]
    ;
    ; setting: server-id
    ; desc   : Sets the server id used to authenticate with Blackfire
    ; default:
    ;
    ; You can find your personal server-id at https://blackfire.io/my/settings/credentials
    server-id=<YOUR_SERVER_ID>

    ;
    ; setting: server-token
    ; desc   : Sets the server token used to authenticate with Blackfire. It is unsafe to set this from the command line
    ; default:
    ;
    ; You can find your personal server-token at https://blackfire.io/my/settings/credentials
    server-token=<YOUR_SERVER_TOKEN>

    ;
    ; setting: log-file
    ; desc   : Sets the path of the log file. Use stderr to log to stderr
    ; default: stderr
    log-file=stderr

    ;
    ; setting: log-level
    ; desc   : log verbosity level (4: debug, 3: info, 2: warning, 1: error)
    ; default: 1
    log-level=1

    ;
    ; setting: memory-limit
    ; desc   : Sets the maximum allowed RAM usage (megabytes) when ingesting traces. Use 0 to disable
    ; default: 500
    memory-limit=500

    ;
    ; setting: socket
    ; desc   : Sets the socket the agent should read traces from. Possible value can be a unix socket or a TCP address
    ;
    ; default Linux:
    ; socket=unix:///var/run/blackfire/agent.sock
    ;
    ; default macOS:
    ; unix:///usr/local/var/run/blackfire-agent.sock
    ;
    ; default Windows:
    ; socket=tcp://127.0.0.1:8307

    ;
    ; setting: ca-cert
    ; desc   : Sets the PEM encoded certificates
    ; default:
    ; ca-cert=

    ;
    ; setting: collector
    ; desc   : Sets the URL of Blackfire's data collector
    ; default: https://blackfire.io
    ; collector=https://blackfire.io

    ;
    ; setting: statsd
    ; desc   : Sets the statsd server to send agent's statistics to. ie: udp://host:port. Leave empty to disable.
    ; default:
    ; statsd=

    ;
    ; setting: statsd-prefix
    ; desc   : Sets the statsd prefix to use when sending data
    ; default: blackfire
    ; statsd-prefix=blackfire

.. _etc-default-blackfire-agent-legacy:

.. warning::

    On Linux machines, setups using our packages also use an additional
    ``/etc/default/blackfire-agent`` configuration file. This allow service
    startup scripts to check settings and create directories or fix permissions
    if required.

    On those configurations, you need to tweak this file to change the socket or
    the log target.

    Here is the default content for this file:

    .. code-block:: bash

        # defaults socket for Blackfire Agent
        SOURCEDIR="/var/run/blackfire"
        SOURCE="unix://${SOURCEDIR}/agent.sock"

        # Log file
        LOG_FILE="/var/log/blackfire/agent.log"

        # User under which the program will run
        USER="blackfire"

        # Arguments that will be given to the program when running it
        DAEMON_ARGS="--log-file=${LOG_FILE} --socket=${SOURCE}"

.. _configuration-agent-legacy-envvars:

Configuring the legacy Agent v1 via Environment Variables
---------------------------------------------------------

The Agent can also be configured using environment variables:

- ``BLACKFIRE_SERVER_ID`` / ``BLACKFIRE_SERVER_TOKEN``

  Sets the server id and server token used to authenticate with Blackfire

  .. include-twig:: `server_credentials`

- ``BLACKFIRE_LOG_LEVEL``

  Sets the verbosity of Agent's log output. Default value is ``1`` (error).

  .. code-block:: bash

    # 1: error, 2: warning, 3: info, 4: debug
    BLACKFIRE_LOG_LEVEL=1

- ``BLACKFIRE_LOG_FILE``

  Sets the output destination of Agent's log. Default value is ``stderr``.

  .. code-block:: bash

    BLACKFIRE_LOG_FILE="/tmp/blackfire-agent.log"

- ``BLACKFIRE_CONFIG``

  Sets the location of the configuration file

  .. code-block:: bash

    BLACKFIRE_CONFIG="/dev/null"

- ``BLACKFIRE_MEMORY_LIMIT``

    Sets the maximum allowed RAM usage (megabytes) when ingesting traces. Use 0 to disable

  .. code-block:: bash

    BLACKFIRE_MEMORY_LIMIT=500

- ``BLACKFIRE_SOCKET``

  Sets the socket the Agent will listen for the probes on.
  Possible values can be a unix socket or a TCP address.

  The default value is platform dependent, as detailed below.

  On Linux:

  .. code-block:: bash

    BLACKFIRE_SOCKET="unix:///var/run/blackfire/agent.sock"

  On macOS:

  .. code-block:: bash

    BLACKFIRE_SOCKET="unix:///usr/local/var/run/blackfire-agent.sock"

  On Windows:

  .. code-block:: bash

    BLACKFIRE_SOCKET="tcp://127.0.0.1:8307"

  On Docker, it is suggested to use this value:

  .. code-block:: bash

    BLACKFIRE_SOCKET="tcp://0.0.0.0:8307"

- ``BLACKFIRE_COLLECTOR``

  Sets the URL of Blackfire's data collector. Default value is ``https://blackfire.io``.

  .. code-block:: bash

    BLACKFIRE_COLLECTOR="https://blackfire.io"

- ``BLACKFIRE_STATSD``

  Sets the statsd server to send agent's statistics to. ie: ``udp://host:port``.

  .. code-block:: bash

    BLACKFIRE_STATSD="udp://host:port"

- ``BLACKFIRE_STATSD_PREFIX``

  Sets the statsd prefix to use when sending data. Default value is ``blackfire``.

  .. code-block:: bash

    BLACKFIRE_STATSD_PREFIX="blackfire"

You can set these environment variables in a project's local ``.env`` file if
supported, or in your global shell configuration file (such as ``~/.bashrc`` or
``~/.zshrc``):

.. code-block:: bash

    export BLACKFIRE_SERVER_ID=xxx
    export BLACKFIRE_SERVER_TOKEN=yyy
    export BLACKFIRE_LOG_LEVEL=4
    export BLACKFIRE_LOG_FILE=/tmp/agent.log

Running the legacy Agent v1 Behind an HTTP(s) Proxy
---------------------------------------------------

.. warning::

    If you are behind a proxy, define the ``HTTP_PROXY`` and/or ``HTTPS_PROXY`` environment variables
    or add the following options to the command: ``--http-proxy`` and/or ``--https-proxy``.
