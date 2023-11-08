You should disable theme debugging in Drupal 7
==============================================

Drupal 7 mostly uses PHP files to render its pages (however it supports
other engines as well). Drupal supports a `debugging mode`_ that outputs
extra information about each template used, to help themers while they
are working on a site. However, generating this extra information slows
down the rendering process.

How To Disable Theme Debug Mode
-------------------------------

Edit your site's ``settings.php`` or ``settings.local.php`` file, which
is usually located in ``sites/default``. Find the line that says:

.. code-block:: php

    $conf['theme_debug'] = TRUE;

Either comment that line out or set it to ``$conf['theme_debug'] = FALSE;``.
Once done, clear your site's caches.

.. _`debugging mode`: https://www.drupal.org/docs/7/theming/overriding-themable-output/working-with-template-suggestions
