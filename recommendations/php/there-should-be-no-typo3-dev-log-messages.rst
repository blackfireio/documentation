There should be no TYPO3 dev-log messages
=========================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

The dev-log should only be used during development for logging and debugging purposes. Make sure to remove those
calls on production environments. For logging on production use the TYPO3 logging framework. For more information
see `TYPO3 Logging Framework Documentation`_.


.. _`TYPO3 Logging Framework Documentation`: https://docs.typo3.org/typo3cms/CoreApiReference/ApiOverview/Logging/Index.html
.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
