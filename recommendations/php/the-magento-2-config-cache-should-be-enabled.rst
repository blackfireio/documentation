The Magento 2 config cache should be enabled
============================================

The configuration of a Magento store, including all its modules, is defined in
lots of different XML files. Collecting these files and merging them to generate
the final configuration used by the application consumes lots of resources.

For that reason, Magento includes a special cache to store and reuse the
processed configuration. This cache also contains store-specific settings stored
in the file system and database. Don't forget to clean or flush this cache type
after modifying configuration files.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Tools > Cache Management and make sure that the **Configuration**
status is **Enabled**.

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable config

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
