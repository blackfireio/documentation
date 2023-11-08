CLI Configuration
=================

.. _configuration-cli:

The Blackfire CLI can be configured via a configuration file, flags passed to
the binary, or environment variables.

Configuring the CLI via a Configuration File
--------------------------------------------

The Blackfire CLI is configured by default with a ``.blackfire.ini`` file that
can be found:

* in ``$BLACKFIRE_HOME/.blackfire.ini`` if you have defined the
  ``$BLACKFIRE_HOME`` environment variable;

* On Linux systems, in ``$XDG_CONFIG_HOME/.blackfire.ini``;

* On all systems, in ``$HOME/.blackfire.ini``;

* On Windows systems, in ``$HOMEDRIVE/$HOMEPATH/.blackfire.ini``.

The most important entries are ``client-id`` and ``client-token``. Here is a
typical configuration for the CLI that you can use as a template:

.. code-block:: ini

    [blackfire]
    ;
    ; setting: client-id
    ; desc   : Sets the Client ID used for API authentication
    ; default: 
    client-id=<YOUR_CLIENT_ID>

    ;
    ; setting: client-token
    ; desc   : Sets the Client Token used for API authentication
    ; default: 
    client-token=<YOUR_CLIENT_TOKEN>

    ;
    ; setting: http-proxy
    ; desc   : Sets the HTTP proxy to use
    ; default: 
    ; http-proxy=

    ;
    ; setting: https-proxy
    ; desc   : Sets the HTTPS proxy to use
    ; default: 
    ; https-proxy=

    ;
    ; setting: endpoint
    ; desc   : Sets the API endpoint
    ; default: https://blackfire.io
    ; endpoint=https://blackfire.io

    ;
    ; setting: timeout
    ; desc   : Sets the Blackfire API connection timeout
    ; default: 15s
    ; timeout=15s

    ;
    ; setting: ca-cert
    ; desc   : Sets the PEM encoded certificates to use
    ; default: 
    ; ca-cert=

Configuring the CLI via Environment Variables
---------------------------------------------

The CLI can also be configured using environment variables:

.. _cli-client-env-vars:

.. include:: _client_env_vars_client_cred.rst
.. include:: _client_env_vars.rst
.. include:: _client_env_vars_example.rst
