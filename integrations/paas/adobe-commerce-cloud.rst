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

:include_twig:`magentocloud_configuration`

.. _trigger-magentocloud:

Builds [level: Production]
--------------------------

.. note::

    Learn more about builds :doc:`in the dedicated documentation
    </builds-cookbooks/index>`.

Follow these steps to enable Blackfire builds on each of your **Adobe Commerce
Cloud environments** each time a branch is deployed (after a ``push``, ``merge``,
or ``redeploy`` event):

:include_twig:`magentocloud_hook`

The command asks several questions. Hit the ``Enter`` key to accept the default
for all of them. If you get a permission error, ask a project admin to
upgrade your account or ask someone who is an admin to run this command.

Now, whenever you push to a Adobe Commerce Cloud environment, Blackfire will
automatically trigger a build for this specific environment. Also, Blackfire
scenarios will be run for all your pull-requests.

Git integration [level: Production]
-----------------------------------

If you are using Github, Bitbucket, or Gitlab, and if you have setup the
synchronization with Adobe Commerce Cloud, don't forget to configure the
:doc:`corresponding notification channel </integrations/git/index>`. That
way, Blackfire can update the status of your pull-requests / merge-requests.

Troubleshooting
---------------

For any issue related to Adobe Commerce Cloud, please check our `dedicated support
documentation <https://support.blackfire.platform.sh/hc/en-us/sections/4843063030162>`_.
