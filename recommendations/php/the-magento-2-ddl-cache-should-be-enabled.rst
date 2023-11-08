The Magento 2 DDL cache should be enabled
=========================================

A `database schema`_ of a database system is its structure described in a formal
language. The schema defines the tables, fields, relationships and indexes of
the database.

The database of Magento applications is both large and complex, so processing
its schema consumes lots of resources. For that reason, Magento includes a
special cache to store and reuse the results of describing tables and indexes.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Tools > Cache Management and make sure that the **Database DDL operations**
status is **Enabled**.

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable db_ddl

This cache is cleaned up automatically when Magento is updated, but if you do
custom changes to the database structure, you should clean or flush the cache
manually.

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`database schema`: https://en.wikipedia.org/wiki/Database_schema
.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
