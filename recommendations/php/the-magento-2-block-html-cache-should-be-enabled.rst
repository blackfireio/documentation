The Magento 2 block HTML cache should be enabled
================================================

Magento applications implement the `Model-View-Controller architecture pattern`_.
Layouts are the major part of the view layer and they define the page structure
using **blocks** and containers.

In practice blocks are defined in layout files and any given Magento application
includes tens of layout files for its themes, modules and components.

Rendering all the blocks included in a page consumes lots of resources.
For that reason, Magento includes a special cache to store the
processed blocks. Some blocks are cachable, some are not.

It is highly recommended to enable the cache of these blocks to improve the
page rendering performance.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Tools > Cache Management and make sure that the **Blocks HTML output**
status is **Enabled**.

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable block_html

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Model-View-Controller architecture pattern`: https://en.wikipedia.org/wiki/Model–view–controller
.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
