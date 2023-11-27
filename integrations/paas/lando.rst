Lando
=====

`Lando <https://lando.dev>`_ is a development platform based on Docker containers,
which dramatically simplifies local development and DevOps.

Blackfire provides an `official plugin for Lando <https://github.com/blackfireio/lando-plugin>`_,
so that you can seamlessly leverage the power provided by Blackfire Profiler and
Lando.

Install
-------

- `Download and extract the archive of the latest version <https://github.com/blackfireio/lando-plugin/releases>`_
  (under ``Assets``, download ``blackfire-lando.zip``);
- Move the extracted ``blackfire`` folder to the Lando plugins folder:

.. code-block:: bash

    mv blackfire ~/.lando/plugins/

.. note::
    If the ``plugins`` directory doesn't exist, create it:

    .. code-block:: bash

        mkdir -p ~/.lando/plugins

Configuration
-------------

1. Configure Blackfire within Lando by setting up a service:

.. include-twig:: `lando_credentials`

2. Rebuild Lando:

.. code-block:: bash

    lando rebuild

Increasing The Log Level
------------------------

If you need to increase the log level for the Blackfire Probe or Agent, you may
configure the ``log_level`` directive:

.. code-block:: yaml

    services:
      blackfire:
        type: blackfire
        # ...
        log_level: 4

Then run ``lando rebuild``.

You can now check the logs:

.. code-block:: bash

    # Blackfire agent log
    lando logs -s blackfire

    # Blackfire probe log, as part of the appserver ones
    lando logs -s appserver

Exposing ``blackfire`` and ``blackfire-player`` as Lando Commands
-----------------------------------------------------------------

When using the Blackfire Lando plugin, ``blackfire`` and ``blackfire-player``
are getting installed in your application container.

You may expose these commands as `Lando Tooling Commands <https://docs.lando.dev/config/tooling.html>`_
using the following snippet in your Landofile:

.. code-block:: yaml

    # .lando.yml
    tooling:
      blackfire:
        # Replace "appserver" by your app container name if needed
        service: appserver

      blackfire-player:
        service: appserver

This snippet makes it possible to run ``blackfire`` and ``blackfire-player``
commands from the application container in the following way:

.. code-block:: bash

    lando blackfire version
    lando blackfire-player run .blackfire.yaml

Custom App Service name
-----------------------

By default, Lando's main app service is called ``appserver``.

If you decided to call it differently, you need to configure the ``blackfire``
service:

.. code-block:: yaml

    services:
      blackfire:
        type: blackfire
        app_service: my_app_service_name

Known Limitations
-----------------

- The probe is automatically installed in PHP application services. For Python,
  you need to install the PIP package and use ``blackfire-python`` instead of
  ``python``.

Next Steps
----------

1. :doc:`Profile with a browser extension </profiling-cookbooks/profiling-http-via-browser>`
   or :doc:`using CLI </profiling-cookbooks/profiling-http-via-cli>`;
2. :doc:`Automate profiling with builds </builds-cookbooks/index>`;
3. Install in production and :doc:`setup Blackfire Monitoring </monitoring-cookbooks/index>`.
