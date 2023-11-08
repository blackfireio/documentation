The Magento 2 config integration API cache should be enabled
============================================================

**Compiled integration APIs configuration of the Store’s Integrations.**

How To Enable this Cache
------------------------

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable config_integration_api

Using the graphical interface, access the Magento **Admin Panel**, then click on
``System > Tools > Cache Management`` and make sure that the **Integration API
configuration** status is **Enabled**.

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
