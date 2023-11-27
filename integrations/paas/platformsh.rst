Platform.sh
===========

Blackfire has built-in support for `Platform.sh <https://platform.sh>`_
projects. The integration is made simpler as Blackfire agent and probe are
installed and enabled by default on all Platform.sh accounts.

Blackfire **server credentials** and the ``.platform.app.yaml`` file should be
configured out of the box for Platform.sh `Obervability Suite
<https://platform.sh/features/observability-suite/>`_ customers. Those steps may
then be ignored. Blackfire integration appears in the project settings in
Platform.sh `console <https://docs.platform.sh/administration/web.html>`_.

Setting-Up Blackfire Credentials In Your Project
------------------------------------------------

Set the Blackfire **server credentials** as environment variables (run this
command from the root directory of your project):

:include_twig:`platformsh_configuration`

.. note::

    You may also use your
    `Platform.sh console <https://docs.platform.sh/administration/web/configure-environment.html#variables>`_

Setting-Up Blackfire Client Credentials to trigger CLI Profiles
---------------------------------------------------------------

The **client credentials** are required to :doc:`trigger profiles with the CLI
</profiling-cookbooks/profiling-http-via-cli>` from your Platform.sh environments.
In this case, set the **client credentials** as environment variables (run this
command from the root directory of your project):

:include_twig:`platformsh_client_configuration`

.. include:: ../../profiling-cookbooks/_cli-profiling-warning.rst

Configuring Your App
--------------------

The configuration of your application depends on its type.

**PHP Application**

Add the ``blackfire`` PHP extension to the ``.platform.app.yaml`` project file:

.. code-block:: yaml

    runtime:
        extensions:
            - blackfire

**Python Application**

.. note::
    Your application must have the `Blackfire Probe
    installed </docs/up-and-running/installation?action=install&mode=full&version=latest&mode=quick&location=local&os=debian&language=python#install-the-python-probe>`_
    as a ``pip`` dependency.

Update your ``.platform.app.yaml`` file to use the ``blackfire-python`` binary
to start your webserver:

.. code-block:: yaml
    :emphasize-lines: 8

    # .platform.app.yaml
    web:
        upstream:
            socket_family: unix
        # Commands are run once after deployment to start the application process.
        commands:
            # Replace "my_app.wsgi" by your actual WSGI script.
            start: "blackfire-python gunicorn -w 4 -b unix:$SOCKET my_app.wsgi:application"

.. _trigger-platformsh:

Builds [level: Production]
--------------------------

To enable Blackfire builds on all of your **Platform.sh environments**
each time a branch is deployed (after a push, merge, or redeploy event), you
need to set up a specific webhook.

To do so, follow these steps:

#. Install the `platform <https://github.com/platformsh/cli>`_ utility

#. Run the following command:

:include_twig:`platformsh_hook`

The command asks several questions. Hit enter to accept the default for all of
them. If you get a permission error, ask a project admin to upgrade your account
or ask someone who is an admin to run this command.

Now, whenever you push to a Platform.sh environment, Blackfire will
automatically trigger a build for this specific environment. Blackfire scenarios
will be run for all your pull requests.

GitHub integration
------------------

If you are using GitHub and if you have setup the synchronization between GitHub
and Platform.sh, don't forget to configure the :ref:`Blackfire GitHub
notification channel <github-notification-channel>`. That way, Blackfire will
post a status on your GitHub pull requests.

Develop on GitHub, Deploy to Platform.sh and Test on Blackfire [level: Production]
----------------------------------------------------------------------------------

Here is a full video tutorial to get you started with the integration of the
three services:

.. include-twig:: `youtube-iframe`
    :title: platformsh-integration-tutorial
    :src: https://www.youtube-nocookie.com/embed/-5icUW9pUH8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 560px
    :height: 315px
