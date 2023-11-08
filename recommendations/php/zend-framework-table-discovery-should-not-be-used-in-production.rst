Zend Framework Table discovery should not be used in production
===============================================================

The ``Adapter`` object is the ``Zend\Db`` sub-component that transforms the PHP
code written to perform database queries into the actual SQL code adapted for
the specific database platform used by the application.

By default, some database operations (``insert()``, ``find()`` and ``info()``)
require this adapter to introspect the metadata of the database tables, such as
their names and columns. This introspection impacts the application performance
because it slows down every database query.

Blackfire detects every call to the ``describeTable()`` method that introspects
the database metadata and warns you when using it in the production environment.
Read the `Caching Table Metadata`_ section in the Zend manual to learn how to
avoid this issue.

.. _`Caching Table Metadata`: https://framework.zend.com/manual/1.12/en/zend.db.table.html#zend.db.table.metadata.caching
