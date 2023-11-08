You should limit the number of PHP files you load in Drupal 8
=============================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

A Drupal 8 site has thousands of files full of PHP code, which work together
to dynamically generate each page. But no page requires every single file to
be loaded. Drupal is efficient about this, loading most files only when their
code is necessary.

If your site is loading too many PHP files, it could mean that you have too many
contrib modules installed. Visit `the page for that recommendation`_ to see what
to do about that.

Alternatively, you might have code that is unnecessarily loading files or
classes. To identify what's loading files, look for callers of
``module_load_include()`` and ``ModuleHandler::loadInclude()``. To identify what's
loading classes, one place to look is anywhere calling
``PluginManager::createInstance()`` in a loop.

.. _`the page for that recommendation`: you-should-not-use-too-many-contrib-modules-in-drupal-8.html
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
