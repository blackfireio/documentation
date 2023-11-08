The Magento 2 DB Logger should not be called on production mode
===============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Agence DnD`_.

The Magento DB Logger allows you to analyze all the SQL queries of the platform.

It must be disabled on production environments for the following reasons:

* Performance: the logger will write in a file all the SQL queries executed on
  platform as well as the details of all the PHP process that led to the request.

* Security: sensitive information can be contained in the requests and in the
  details of the PHP process.

You can disable it with the following line: ``bin/magento dev:query-log:disable``.


.. _`a contribution by Agence DnD`: https://www.blackfire.io/labels/contributor/
