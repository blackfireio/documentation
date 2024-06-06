DDEV
====

`DDEV <https://ddev.com>`_ is a development platform for PHP based on Docker
containers (`DDEV-Local <https://ddev.com/ddev-local/>`_).

DDEV-Local
----------

You must use version 1.17 or above of DDEV-local.
Their `documentation <https://ddev.readthedocs.io/en/stable/#installation>`_
offers detailed procedures for most OSes.

Configuration
-------------

The Blackfire probe is installed by default and the agent is added as an
additional service. It can be configured globally with this command:

.. include-twig:: `ddev_credentials`

The credentials can be configured for a specific project by updating its
`DDEV config file <https://ddev.readthedocs.io/en/latest/users/configuration/config/>`_
located in ``.ddev/config.yaml``:

.. include-twig:: `ddev_credentials_config`

Restart DDEV
------------

.. code-block:: bash
    :zerocopy:

    ddev restart

Activate Blackfire
------------------

To activate Blackfire after every ``ddev restart``, run the following command:

.. code-block:: bash
    :zerocopy:

    ddev blackfire

To activate Blackfire every time your project starts, in the ``.ddev/config.yml``
file of your DDEV project, define a custom `hook <https://ddev.readthedocs.io/en/stable/users/configuration/hooks/>`_
similar to:

.. code-block:: yaml
    :zerocopy:

    # .ddev/config.yml

    hooks:
        post-start:
            - exec-host: 'ddev blackfire'


Additional commands:

- Disable the Blackfire Probe and stops the Blackfire agent
  (this can be useful if you need to run xdebug, which is deactivated when you start
  Blackfire  with ``ddev blackfire``):

.. code-block:: bash
    :zerocopy:

    ddev blackfire off

- Verify if Blackfire is currently enabled, as well as the currently installed:
  Blackfire Probe version.

.. code-block:: bash
    :zerocopy:

    ddev blackfire status

You can now profile requests with :doc:`all available methods </profiling-cookbooks/index>`.
When profiling with the CLI, prefix the ``blackfire`` commands with ``ddev exec``:

- ``ddev exec blackfire curl https://foobar.ddev.site``
- ``ddev exec blackfire drush st``

.. note::

    When using ``ddev exec blackfire curl http://127.0.0.1``, there is no need
    to specify a DDEV external port as you are already executing it in a DDEV
    context. Additional documentation is provided by `ddev-contrib
    <https://ddev.readthedocs.io/en/latest/users/blackfire-profiling/>`_.

.. _ddev-player:

Blackfire Player
-----------------

:doc:`Blackfire Player </builds-cookbooks/player>` can be used in your DDEV
project to trigger automated performance tests or crawl information.

DDEV support `custom commands <https://ddev.readthedocs.io/en/stable/users/extend/custom-commands/>`_
enriching its standard behavior. Let's setup a ``ddev player`` command for a
project by creating it configuration file ``.ddev/commands/host/player`` with this
content:

.. include-twig:: `blackfire_player_ddev`
