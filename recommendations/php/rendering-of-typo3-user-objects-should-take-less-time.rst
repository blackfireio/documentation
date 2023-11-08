Rendering of TYPO3 user objects should take less time
=====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

A TYPO3 user object (usually a TYPO3 extension's frontend plugin) should not take too much time as compared to
the rendering of the rest of the site. If only one extension takes up the majority of the rendering time it would be
wise to check that extension for performance drains.

.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
