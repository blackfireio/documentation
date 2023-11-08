The Magento 2 full page cache should be enabled
===============================================

Magento is a database-driven application which generates contents dynamically.
However, when some page contents don't change frequently and when you have lots
of visitors, generating the same page repeatedly is a waste of server resources.

This problem can be solved with one of the several caches included in Magento
which is called **Page Cache**. This cache turns dynamic contents into fully
cacheable static HTML contents, improving the application performance dramatically.

When enabled, this page cache is only applied to public pages such as CMS
contents, product pages and categories. Private pages such as user accounts or
carts are never cached. Since cached pages usually contain some bits of private
information, such as the name of the logged customer, Magento performs Ajax
requests to fill in the static cached page with all the needed private
information.

Magento cleans this cache automatically when needed, but you can force a clean
or "flush" of this cache after modifying any code that affects HTML output. In
addition, if a page contains at least one layout block with the ``cacheable=false``
attribute, it won't be cached.

How To Enable this Cache
------------------------

Using the graphical interface, access the Magento **Admin Panel**, then click on
System > Tools > Cache Management and make sure that the **Page Cache** status
is **Enabled**.

Using the command console, open a terminal, access your Magento directory and
execute this command:

.. code-block:: bash

    magento cache:enable full_page

Additional Resources
--------------------

* `Manage the cache`_ (Magento Developer Documentation)

.. _`Manage the cache`: https://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cache.html
