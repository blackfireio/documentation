The Magento 2 EAV cache should be enabled
=========================================

In traditional web applications, database tables have a fixed number of columns.
In generic eCommerce applications, this model doesn't fit well because the
attributes needed to describe the products are completely different depending upon
the store type (e.g. a clothing store, a travel agency or a home appliances store).

Magento solves this problem applying an `Entity-Attribute-Value model (EAV)`_,
which is *"a data model that is used in circumstances where the number of attributes
that can be used to describe entities is potentially very vast, but the number
that will actually apply to a given entity is relatively modest"*.

Magento entities define their EAV attributes and the metadata for each attribute;
such as the type of data which stores, the label displayed to describe it,
whether is required or optional, etc.

Processing all these attributes and metadata consumes lots of resources. For
that reason, Magento includes a special cache to store and reuse the processed
EAV attributes.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Tools > Cache Management and make sure that the **EAV types and attributes**
status is **Enabled**.

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable eav

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Entity-Attribute-Value model (EAV)`: https://en.wikipedia.org/wiki/Entity–attribute–value_model
.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
