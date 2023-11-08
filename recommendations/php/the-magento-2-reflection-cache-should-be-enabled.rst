The Magento 2 reflection cache should be enabled
================================================

**Removes a dependency between the Webapi module and the Customer module.**

How To Enable this Cache
------------------------

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable reflection

Using the graphical interface, access the Magento **Admin Panel**, then click on
``System > Tools > Cache Management`` and make sure that the **Reflection** status is
**Enabled**.

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
