You should disable Twig debugging in Drupal 8
=============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal 8 uses the `Twig`_ template engine to render its pages. Drupal supports
a `debugging mode`_ that outputs extra information about each template used,
to help themers while they are working on a site. However, generating this
extra information slows down the rendering process.

How To Disable Twig Debug Mode
------------------------------

Find the ``services.yml`` file, usually located in ``sites/default``. Find
where it says:

.. code-block:: yaml

    parameters:
      twig.config:
        debug: true

Change that to ``debug: false``. Then clear your site's caches.

.. _`Twig`: https://twig.symfony.com/
.. _`debugging mode`: https://www.drupal.org/docs/8/theming/twig/debugging-twig-templates
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
