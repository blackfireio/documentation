OPcache "save_comments" should be enabled on Magento 2
======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Agence DnD`_.


The `opcache.save_comments`_ option allows OPcache to keep code comments in the
cache. It must be enabled on all environments for quality reasons. Many
applications including Magento rely on these comments in their internal logic.
It is therefore important to keep them activated to ensure that the platform
works properly.

You can enable this option with the following line: `opcache.save_comments=1`.

.. _`opcache.save_comments`: https://www.php.net/manual/en/opcache.configuration.php#ini.opcache.save-comments
.. _`a contribution by Agence DnD`: https://www.blackfire.io/labels/contributor/
