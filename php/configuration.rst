Configuration [language: PHP]
=============================

.. _configuration-probe-php:

Configuring the Probe via Environment Variables
-----------------------------------------------

It's preferable that you configure the PHP probe using environment variables.
It allows you to change the configuration without modifying your code.
You can use the following environment variables:

.. include:: /up-and-running/configuration/_client_env_vars_client_cred.rst

- ``BLACKFIRE_DEBUG_SIGSEGV_HANDLER``

  Add the stacktrace to the probe logs when a segmentation fault occurs.

  Default value is ``0`` (stacktrace not collected).

  This debug option is inactive on Windows and Alpine.

  .. code-block:: bash

    BLACKFIRE_DEBUG_SIGSEGV_HANDLER=0

.. include:: /up-and-running/configuration/_client_env_vars.rst
.. include:: /up-and-running/configuration/_client_env_vars_server_cred.rst
.. include:: /up-and-running/configuration/_client_env_vars_example.rst
.. include:: /up-and-running/configuration/_client_ini_defaults.rst

Configuring the Probe via the php.ini Configuration File
--------------------------------------------------------

You can also configure the PHP probe via your ``php.ini`` configuration file:

.. code-block:: ini

    [blackfire]
    extension=blackfire.so
    ; On Windows use the following configuration:
    ; extension=php_blackfire.dll

    ; Sets fine-grained configuration for Probe.
    ; This should be left blank in most cases. For most installs,
    ; the server credentials should only be set in the agent.
    ;blackfire.server_id =

    ; Sets fine-grained configuration for Probe.
    ; This should be left blank in most cases. For most installs,
    ; the server credentials should only be set in the agent.
    ;blackfire.server_token =

    ; Log verbosity level:
    ;   4: debug
    ;   3: info
    ;   2: warning;
    ;   1: error
    ;blackfire.log_level = 1

    ; Log file (STDERR by default)
    ;blackfire.log_file = /tmp/blackfire.log

    ; Add the stacktrace to the probe logs when a segmentation fault occurs.
    ; Debug option inactive on Windows and Alpine.
    ;blackfire.debug.sigsegv_handler = 0

    ; Sets the socket where the agent is listening.
    ; Possible value can be a unix socket or a TCP address.
    ; Defaults values are:
    ;   - Linux: unix:///var/run/blackfire/agent.sock
    ;   - macOS amd64: unix:///usr/local/var/run/blackfire-agent.sock
    ;   - macOS arm64 (M1): unix:///opt/homebrew/var/run/blackfire-agent.sock
    ;   - Windows: tcp://127.0.0.1:8307
    ;blackfire.agent_socket = unix:///var/run/blackfire/agent.sock

    ; Enables Blackfire Monitoring
    ; Enabled by default since version 1.61.0
    ;blackfire.apm_enabled = 1

.. note::

    If you don't know where your ``php.ini`` file is located, run this
    command: ``php --ini``

.. caution::

    **We do not recommend configuring server credentials via** ``php.ini``.

    Make sure you configure your server credentials (server ID and server token)
    in the Agent. This prevents your server credentials from being shared amongst
    all virtual hosts.

    Only configure your server credentials via ``php.ini`` if you have multiple
    Blackfire environments, each with a dedicated server, and all your servers
    are configured to communicate with the same agent.

    In other specific cases, you might want to configure different credentials on
    a per-host/per-directory basis.

Configuring the Probe via the Web Server Configuration
------------------------------------------------------

Make sure you configure your server credentials ``blackfire.server_id`` and
``blackfire.server_token`` in the agent. Only configure your server credentials on
a virtual host-by-virtual host basis if you meet one of the following sets of
requirements:

- You have multiple Blackfire environments, multiple virtual hosts on a server,
  and want to assign specific Blackfire environments to specific virtual hosts.

- You have one or more Blackfire environments, multiple virtual hosts on a server,
  and want to only allow Blackfire profiling on a subset of your virtual hosts.

.. caution::

    The default credentials set in the Agent are used as default fallback, so
    **do not** set default credentials in your ``php.ini`` file.

Nginx Configuration Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can override the default credentials of the Probe in the Nginx
configuration via the ``http``, ``server``, and ``location`` sections. For more
information, see the `Nginx documentation
<https://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_param>`_.

.. include-twig:: `php_nginx`

.. note::

    Make sure you configure **all the hosts** served by a PHP-FPM pool.

.. tip::

    If you want a host to use the default credentials, set empty values:

    .. code-block:: text

        location / {
          fastcgi_param PHP_VALUE "
            blackfire.server_id=
            blackfire.server_token=
        ";
        }

Apache Configuration Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can override the default credentials of the Probe in the main Apache
virtual-host configuration or via a ``.htaccess`` file.

Use the following example to adjust your configuration. For more information, see
the `PHP documentation <https://www.php.net/manual/en/configuration.changes.php>`_.

.. include-twig:: `php_apache`

PHP-FPM Pool Configuration Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can override the default credentials of the Probe per PHP-FPM pool. Open the
``php-fpm.conf`` file and amend the settings. Use the following example for
reference or the `FPM documentation
<https://www.php.net/manual/en/install.fpm.configuration.php>`_.

.. include-twig:: `php_fpm`

.. note::
    :class: doc-cta

    If your app is behind a cache server, a load balancer, or any other reverse
    proxy, make sure you :doc:`bypass it </up-and-running/reverse-proxies>`.
