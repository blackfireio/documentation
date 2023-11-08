On a cached TYPO3 page, no individual content elements should be rendered
=========================================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

You should always strive to deliver fully cached TYPO3 pages - even if it's only for a few minutes. If there is
even a single uncached element on the page TYPO3 will have to run through a lot more bootstrapping to be able to
render parts of the website from cache and process the uncached part - it has to load configuration options,
initialize the correct context, evaluate display conditions and more. If the whole page comes from the cache
there is no rendering process and the whole website will be delivered much faster. Think about your content and
whether it really is uncachable. Most of the times, you may trigger regenerating of the cache on specific events
(data changed through an import, an editor changing content ...) via cache tags or set the lifetime of your caches
to a pretty low value (even caching for 5 minutes helps).

For more information have a look at the `documentation of the caching framework`_.

.. _`documentation of the caching framework`: https://docs.typo3.org/typo3cms/CoreApiReference/CachingFramework/Index.html
.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
