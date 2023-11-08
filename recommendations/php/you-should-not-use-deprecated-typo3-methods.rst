You should not use deprecated TYPO3 methods
===========================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

You should not use deprecated methods, as they will always trigger a call to the deprecation logger costing you a
tiny bit of performance due to that call. Additionally they will prevent your application from being updated to newer
TYPO3 versions.

To find out where the deprecations are coming from enable the deprecation log via the install tool and make sure to
remove all calls listed there. If those calls are related to third party extensions find out whether there is an
updated version available or create an issue and/or pull request for that extension.

.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
