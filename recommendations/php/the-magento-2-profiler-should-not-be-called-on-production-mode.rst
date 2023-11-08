The Magento 2 Profiler should not be called on production mode
==============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Agence DnD`_.

The Magento profiler is used to analyze the performance of the platform. It
must be disabled on production environments for the following reasons:

* Performance: The profiler will store all the information to be displayed in
  the output during the application runtime. This takes memory and processing
  time.

* Security: The profiler will display sensitive information such as:
    * PHP classes
    * Template files
    * Observers and events
    * Layouts
    * Controllers

You can disable it with the following line: ``bin/magento dev:profiler:disable``.

.. _`a contribution by Agence DnD`: https://www.blackfire.io/labels/contributor/
