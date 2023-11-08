You should enable twig cache in Drupal 8
============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Smile`_.

Drupal 8 uses the `Twig`_ template engine to render its pages. Disabling Drupal 8
caching (render cache, dynamic page cache, Twig cache) during development is useful
for seeing changes without clearing the cache.

Disabling these three caches helps speed up development and reduce confusion.

How To Enable twig Cache
------------------------

Find the ``services.yml`` file, usually located in ``sites/default``. Find
where it says:

.. code-block:: yaml

    parameters:
      twig.config:
        cache: false

Change that to ``cache: true``. Then clear your site's caches.

.. _`Twig`: https://twig.symfony.com/
.. _`Drupal twig`: https://www.drupal.org/docs/8/theming/twig/debugging-twig-templates
.. _`a contribution by Smile`: https://www.adyax.com/
