You should do less non-cached calls to Ibexa SPI handlers
===============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by ibexa.co`_.

Some of the SPI persistence cache handlers are not cached by design
and it could lead to larger amount of SQL queries.
You can read more about persistence cache at `Persistence cache`_, SPI at `SPI and API repositories`_
and on related recommendation:

* :doc:`SPI database persistence handlers calls </recommendations/php/you-should-do-less-calls-with-ibexa-spi-handlers>`

.. _`Persistence cache`: https://doc.ibexa.co/en/latest/infrastructure_and_maintenance/cache/persistence_cache/#__toc
.. _`SPI and API repositories`: https://doc.ibexa.co/en/3.3/guide/repository/#spi
.. _`a contribution by ibexa.co`: https://blog.blackfire.io/ez-platform-recommendations.html
