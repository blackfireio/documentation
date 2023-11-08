- ``BLACKFIRE_AGENT_SOCKET``

  Defines which socket the Probe contacts the Agent on.
  Possible values can be a Unix socket or a TCP address.

  The default value is platform dependent, as detailed below.

  On Linux:

  .. code-block:: bash

    BLACKFIRE_AGENT_SOCKET="unix:///var/run/blackfire/agent.sock"

  On macOS:

  .. code-block:: bash

    # amd64
    BLACKFIRE_AGENT_SOCKET="unix:///usr/local/var/run/blackfire-agent.sock"

    # arm64 (M1)
    BLACKFIRE_AGENT_SOCKET="unix:///opt/homebrew/var/run/blackfire-agent.sock"

  On Windows:

  .. code-block:: bash

    BLACKFIRE_AGENT_SOCKET="tcp://127.0.0.1:8307"

- ``BLACKFIRE_ENDPOINT``

  Defines which API endpoint the profile data is sent to.

  .. code-block:: bash

    BLACKFIRE_ENDPOINT="https://blackfire.io"

- ``BLACKFIRE_APM_ENABLED``

  Enables or disables Blackfire Monitoring.

  .. code-block:: bash

    BLACKFIRE_APM_ENABLED=1
