You should do less calls to the TYPO3 Condition Matcher
=======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

Using a lot of TypoScript conditions in TYPO3 results in an exponential growth of the caching table therefore
slowing down the system. Think carefully on which conditions you need and whether those could be reduced or solved
differently.

.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
