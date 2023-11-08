The Magento 2 collections cache should be enabled
=================================================

Collection cache results from database queries. Magento cleans it up
automatically whenever needed, but third-party developers can put data in
any segment of this cache.
You may clean up or flush this cache type if your custom module generates cache
entries which Magento cannot clean up.

How To Enable this Cache
------------------------

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable collections

Using the graphical interface, access the Magento **Admin Panel**, then click on
`System > Tools > Cache Management` and make sure that the **Collections data** status is
**Enabled**.

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
