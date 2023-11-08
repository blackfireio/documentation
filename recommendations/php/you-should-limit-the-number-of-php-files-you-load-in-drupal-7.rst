You should limit the number of PHP files you load in Drupal 7
=============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

A Drupal 7 site has thousands of files full of PHP code, which work together
to dynamically generate each page. But no page requires every single file to
be loaded. Drupal is efficient about this, loading most files only when their
code is necessary.

If your site is loading too many PHP files, it could mean that you have too many
contrib modules installed. Visit `the page for that recommendation`_ to see what
to do about that.

Alternatively, you might have code that is unnecessarily loading files or
classes. To identify what's loading files, look for callers of these functions
in a debugger:

* ``module_load_include()``
* ``drupal_autoload_class()``
* ``drupal_autoload_interface()``
* ``drupal_autoload_trait()``

.. _`the page for that recommendation`: you-should-not-use-too-many-contrib-modules-in-drupal-7.html
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
