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

.. include-twig:: `upsun_client_configuration`

.. include:: ../../profiling-cookbooks/_cli-profiling-warning-simplified.rst

Develop on GitHub, Deploy to Upsun and Test on Blackfire
--------------------------------------------------------

Here is a full video tutorial to get you started with the integration of the
three services:

.. include-twig:: `youtube-iframe`
    :title: upsun-integration-tutorial
    :src: https://www.youtube-nocookie.com/embed/-5icUW9pUH8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 560px
    :height: 315px
