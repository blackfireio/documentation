Upsun
=====

A full access to Blackfire is bundled with your PHP and Python Upsun projects.

Blackfire has built-in support for `Upsun <https://upsun.com>`__
projects. The integration is made simpler as Blackfire agent and probe are
installed and enabled by default on all Upsun projects.

Blackfire **server credentials** are automatically configured on all PHP and Python
Upsun projects. The Blackfire integration appears in the project settings in
Upsun `console <https://docs.upsun.com/administration/web.html>`_.

Monitoring
----------

Blackfire monitoring is enabled by default on your production environment.

To enable Blackfire monitoring on your development or staging environments,
go to your organization menu and click :ref:`Organization Monitoring Usage <monitoring-activation>`

CLI Profiling
-------------

HTTP requests can be profiled without any extra configuration, but the 
**client credentials** are required to :doc:`trigger profiles with the CLI
</profiling-cookbooks/profiling-http-via-cli>` from your Upsun environments.

Set the **client credentials** as environment variables (run this
command from the root directory of your project):

:include_twig:`upsun_client_configuration`

.. include:: ../../profiling-cookbooks/_cli-profiling-warning-simplified.rst

.. _trigger-upsun:

Builds
------

To enable Blackfire builds on all of your **Upsun environments**
each time a branch is deployed (after a push, merge, or redeploy event), you
need to set up a specific webhook.

To do so, follow these steps:

#. Install the `Upsun <https://docs.upsun.com/administration/cli.html>`_ CLI.

#. Run the following command:

:include_twig:`upsun_hook`

The command asks several questions. Hit enter to accept the default for all of
them. If you get a permission error, ask a project admin to upgrade your account
or ask someone who is an admin to run this command.

Now, whenever you push to an Upsun environment, Blackfire will
automatically trigger a build for this specific environment. Blackfire scenarios
will be run for all your pull requests.

GitHub integration
------------------

If you are using GitHub and if you have setup the synchronization between GitHub
and Upsun, don't forget to configure the :ref:`Blackfire GitHub
notification channel <github-notification-channel>`. That way, Blackfire will
post a status on your GitHub pull requests.

Develop on GitHub, Deploy to Upsun and Test on Blackfire
--------------------------------------------------------

Here is a full video tutorial to get you started with the integration of the
three services:

.. raw:: html

    <iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/-5icUW9pUH8?rel=0&showinfo=0&modestbranding=1&autoplay=0" frameborder="0" allowfullscreen></iframe>
