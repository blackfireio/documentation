You should leave all caches enabled in Drupal 7
===============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

A Drupal site uses data from many different places: PHP files, INI files,
the database, and more. Reading and processing all those files on every page
load would be much too slow, so Drupal keeps it cached in several different
**cache bins**.

Sometimes this is inconvenient for developers, as it forces them to regularly
clear their caches for each small change they make. So developers will
sometimes `disable certain caches`_ while they make certain changes. However,
all caches should always be enabled in production, and almost always even in
development.

How To Re-enable Caches
-----------------------

Examine your ``settings.php`` and ``settings.local.php`` files, usually
located in ``sites/default``. Look for lines that reference
``DrupalFakeCache``, like this one:

.. code-block:: php

    $conf['cache_default_class'] = 'DrupalFakeCache';

Comment out or remove those lines, and then clear your caches.


.. _`disable certain caches`: https://www.drupal.org/docs/7/creating-custom-modules/suppress-caching-for-development-or-to-use-an-external-page-cache
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
