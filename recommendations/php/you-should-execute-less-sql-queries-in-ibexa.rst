You should execute less SQL queries in Ibexa
==================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by ibexa.co`_.

Ibexa has a optimized repository cable of reliably caching persistence _(database)_
lookups to the database using SPI Persistence Cache, and cable of using Solr for API Search queries.
Too many SQL queries indicates that you might not be properly taking advantage of these features,
potentially slowing down your system.

You can read more in related recommendations:

* :doc:`SPI database persistence handlers calls </recommendations/php/you-should-do-less-calls-with-ibexa-spi-persistence-legacy-database-handlers>`
* :doc:`SPI handlers calls </recommendations/php/you-should-do-less-calls-with-ibexa-spi-handlers>`
* :doc:`Service Repository calls </recommendations/php/you-should-do-less-calls-to-ibexa-service-repository>`

.. _`a contribution by ibexa.co`: https://blog.blackfire.io/ez-platform-recommendations.html
