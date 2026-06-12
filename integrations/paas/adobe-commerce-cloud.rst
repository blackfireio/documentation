Adobe Commerce Cloud
====================

Blackfire has built-in support for `Adobe Commerce Cloud
<https://devdocs.magento.com/cloud/bk-cloud.html>`_ projects.

The Blackfire Agent is already installed and enabled by default on all Adobe
Commerce Cloud accounts.

Configuration
-------------

To activate the Blackfire Probe on integration branches, add the ``blackfire``
PHP extension in your ``.magento.app.yaml`` project file:

   .. code-block:: yaml

       runtime:
           extensions:
               - blackfire

   .. note::

       The Blackfire Probe can be installed and enabled by developers on any
       branch in the `Starter architecture <https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/architecture/starter-architecture.html?lang=en>`_
       and only integration branches on `Pro architecture <https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/architecture/pro-architecture.html?lang=en>`_.

       To install it on dedicated Staging and Production environments on
       `Pro architecture <https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/architecture/pro-architecture.html?lang=en>`_ submit a request
       to `Adobe Commerce help center <https://support.magento.com/>`_.

Set the Blackfire **server credentials** as environment variables, for each
branch on which you want to configure Blackfire.

.. include-twig:: `magentocloud_configuration`

.. _trigger-magentocloud:

Synthetic monitoring [level: Production]
----------------------------------------

To verify performance on each deployment, run
:doc:`Blackfire Player </builds-cookbooks/synthetic-monitoring>` with the
``--report`` option from your Adobe Commerce Cloud deploy hook or CI pipeline.
Point Player at the deployed environment with ``--endpoint`` so it profiles your
scenarios after every ``push``, ``merge``, or ``redeploy`` event, and gate the
job on its exit code.

Troubleshooting
---------------

For any issue related to Adobe Commerce Cloud, please check our `dedicated support
documentation <https://support.blackfire.platform.sh/hc/en-us/sections/4843063030162>`_.
