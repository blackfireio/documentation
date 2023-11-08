.. warning::
    Recommended: To explicitly define which
    :doc:`environment </reference-guide/environments>` the profile must be sent
    to, use the ``--env=<ENV_UUID>`` parameter.

    Blackfire Agent uses the ``BLACKFIRE_SERVER_ID`` environment variable to
    determine where to send the profile.

    When no target environment is specified or implicitly discovered, the profile
    is sent to the personal sandbox environment of the user whose
    :ref:`personal credentials <cli-client-env-vars>` (``BLACKFIRE_CLIENT_ID``
    and ``BLACKFIRE_CLIENT_TOKEN``) were used. Only that user can then access
    the profile from `/my/profiles </my/profiles>`_.

    To explicitly specify your personal sandbox environment, use
    ``--env="My Environment"``
