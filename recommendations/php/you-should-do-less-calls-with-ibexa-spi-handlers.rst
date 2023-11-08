You should do less calls with Ibexa SPI handlers
======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by ibexa.co`_.

SPI handlers are used by Service Repositories to store/retrieve data from Storage Engine.

Keep in mind that some of the SPI handlers are not cached:

* :doc:`SPI database persistence handlers calls </recommendations/php/you-should-do-less-calls-with-ibexa-spi-handlers>`

You can read more at `Persistence cache`_ and `SPI and API repositories`_.

.. _`Persistence cache`: https://doc.ibexa.co/en/latest/guide/persistence_cache/#__toc
.. _`SPI and API repositories`: https://doc.ibexa.co/en/latest/guide/repository/#spi
.. _`a contribution by ibexa.co`: https://blog.blackfire.io/ez-platform-recommendations.html
