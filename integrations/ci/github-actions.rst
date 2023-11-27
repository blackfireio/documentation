GitHub Actions
==============

`GitHub Actions <https://github.com/features/actions>`_ is a continuous
integration platform that comes with `GitHub <https://github.com/>`_.

Integrating Blackfire with GitHub Actions enables running Blackfire tests and
scenarios, through :doc:`PHPUnit tests </php/integrations/phpunit>`, the
:doc:`Blackfire Player </builds-cookbooks/player>`, or the :ref:`Blackfire CLI
Tool <configuration-cli>`. It also makes it possible to :ref:`trigger Blackfire
builds <build-webhook>`.

.. note::

    GitHub Actions support is available, via the `setup-php
    action <https://github.com/marketplace/actions/setup-php-action>`_.

    While this action is designed for PHP, it installs all needed components,
    making Blackfire **usable by apps written in any language supported by
    Blackfire** (Python, Go...).

Configuring the Project
-----------------------

To set up Blackfire on GitHub Actions, you need to define some `secret
variables in your project settings
<https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets>`_.

Define secrets for your **Client** credentials:

.. include-twig:: `client_credentials`

Define secrets for the **Server** credentials. Select the Blackfire
environment which you want to use for your GitHub Actions-triggered tests:

.. include-twig:: `server_credentials`

Configuring your Job
--------------------

Within your workflow, configure each job where you need Blackfire:

.. code-block:: yaml

    jobs:
      build:
        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v2

        - name: Setup Blackfire via setup-php Action
          uses: shivammathur/setup-php@v2
          with:
            # PHP Only: Setup PHP extensions, including Blackfire Probe.
            # It is recommended to disable xdebug.
            # Not needed for other languages.
            extensions: blackfire, :xdebug
            # Setup Blackfire Agent and CLI tool, and Blackfire Player
            tools: blackfire, blackfire-player
          env:
            # Expose your Blackfire credentials stored in secrets
            # as environment variables.
            BLACKFIRE_SERVER_ID: ${{ secrets.BLACKFIRE_SERVER_ID }}
            BLACKFIRE_SERVER_TOKEN: ${{ secrets.BLACKFIRE_SERVER_TOKEN }}
            BLACKFIRE_CLIENT_ID: ${{ secrets.BLACKFIRE_CLIENT_ID }}
            BLACKFIRE_CLIENT_TOKEN: ${{ secrets.BLACKFIRE_CLIENT_TOKEN }}

        # Trigger a profile using Blackfire CLI tool.
        - name: Profile list-users command
          env:
            APP_ENV: prod
            APP_DEBUG: 0
          run: blackfire run php bin/console app:list-users
          # Other example using Python:
          #run: blackfire run python my_script.py

Use option ``--env`` to target a specific environment (:ref:`see documentation
<profiling-cli-specifying-target-environment>`).

Using Blackfire Player [level: Production]
------------------------------------------

Thanks to the `setup-php action <https://github.com/marketplace/actions/setup-php-action>`_,
you can :doc:`use Blackfire Player to run your scenarios and get build reports
</integrations/blackfire-player>` each time you push a new version of your
code on GitHub. ``setup-php`` also supports the Symfony CLI tool. This
enables you to start the Symfony local webserver so that you can execute the
Blackfire Player scenarios directly from your running job.

.. note::

    When using other languages than PHP, e.g. Python, you may use other
    webservers like ``gunicorn`` or the Django development server.

.. code-block:: yaml

    jobs:
      build:
        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v2

        - name: Setup Blackfire via setup-php Action
          uses: shivammathur/setup-php@v2
          with:
            php-version: '7.4'
            extensions: blackfire, :xdebug
            # Setup Blackfire Agent and CLI tool, Blackfire Player, and Symfony CLI
            tools: blackfire, blackfire-player, symfony
          env:
            BLACKFIRE_SERVER_ID: ${{ secrets.BLACKFIRE_SERVER_ID }}
            BLACKFIRE_SERVER_TOKEN: ${{ secrets.BLACKFIRE_SERVER_TOKEN }}
            BLACKFIRE_CLIENT_ID: ${{ secrets.BLACKFIRE_CLIENT_ID }}
            BLACKFIRE_CLIENT_TOKEN: ${{ secrets.BLACKFIRE_CLIENT_TOKEN }}

        - name: Symfony local server start
          env:
            APP_ENV: prod
            APP_DEBUG: 0
          run: |
            symfony local:server:start -d # Start Symfony local webserver
            # Run Blackfire Player scenarios from .blackfire.yaml or .bkf files
            blackfire-player run --endpoint=http://localhost:8000 --blackfire-env=<your-blackfire-environment-id> .blackfire.yaml

Triggering a Blackfire Build [level: Production]
------------------------------------------------

`setup-php action <https://github.com/marketplace/actions/setup-php-action>`_
supports the ``blackfire`` CLI tool. It enables to :ref:`trigger a Blackfire build
<build-webhook-trigger>`:

.. code-block:: yaml

    jobs:
      build:
        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v2

        - name: Setup PHP Action
          uses: shivammathur/setup-php@v2
          with:
            # Setup Blackfire Agent and CLI tool and Blackfire Player
            tools: blackfire, blackfire-player
          env:
            BLACKFIRE_SERVER_ID: ${{ secrets.BLACKFIRE_SERVER_ID }}
            BLACKFIRE_SERVER_TOKEN: ${{ secrets.BLACKFIRE_SERVER_TOKEN }}
            BLACKFIRE_CLIENT_ID: ${{ secrets.BLACKFIRE_CLIENT_ID }}
            BLACKFIRE_CLIENT_TOKEN: ${{ secrets.BLACKFIRE_CLIENT_TOKEN }}

        - name: Trigger a Blackfire Build
          run: |
            blackfire build-trigger <ENDPOINT> --env=<ENV-UUID> --token=<TOKEN-VALUE>
