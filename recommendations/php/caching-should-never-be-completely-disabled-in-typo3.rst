Caching should never be completely disabled in TYPO3
====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

TYPO3 has an intricate set of caches to ensure high performance delivery of your websites. Disabling all caches should
under no circumstances be necessary. You should find out where the caching was disabled and re-enable it. If you have
problems with cached information afterwards, you should selectively analyze which caches are the problem and ideally
use cache tags and lifetime configurations to solve those problems.

.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
