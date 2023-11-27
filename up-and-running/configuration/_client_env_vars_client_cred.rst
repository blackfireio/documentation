- ``BLACKFIRE_CLIENT_ID`` / ``BLACKFIRE_CLIENT_TOKEN``

  Sets the client ID and client Token used to authenticate with Blackfire.

  .. include-twig:: `client_credentials`

- ``BLACKFIRE_LOG_LEVEL``

  Sets the verbosity of the Probe's log output. Default value is ``1`` (error).

  .. code-block:: bash

    # 1: error
    # 2: warning
    # 3: info
    # 4: debug
    BLACKFIRE_LOG_LEVEL=1

- ``BLACKFIRE_LOG_FILE``

  Defines where the output of the probe logs is sent. Default value is empty.

  .. code-block:: bash

    BLACKFIRE_LOG_FILE="/tmp/probe.log"
