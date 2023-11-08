You should limit the number of blocks you use in Drupal 8
=========================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal allows you to place boxes of content called **blocks** in different
positions on your site. In Drupal 8, many parts of a page are actually blocks;
the title of a node, the menus, the breadcrumbs, the search field, and more.
Configuring blocks is an extremely flexible way to build a site: Drupal lets
you reorder blocks, place them in different parts of the page, and set
conditions for when each block should or should not appear.

When Drupal shows a page, it has to figure out which blocks to show you. To do
this, it loads every block in your theme and goes through the conditions you
configured on each block. It turns out that loading all the blocks and
evaluating all the conditions can be slow, and this has to happen on every page
load. If you have a limited number of blocks, this won't be too bad. But if you
configure your site with hundreds of blocks, calculating out which ones are
visible can take awhile.

If you find yourself with hundreds of small blocks that display conditionally,
consider finding other options. You could use a module like `Paragraphs`_ or
`Inline Entity Form`_ that uses fields instead of blocks. Or you could use
a module like `Context`_ or `Block Visibility Groups`_ that applies conditions
to blocks in groups, so that Drupal has to calculate fewer conditions.

.. _`Paragraphs`: https://www.drupal.org/project/paragraphs
.. _`Inline Entity Form`: https://www.drupal.org/project/inline_entity_form
.. _`Context`: https://www.drupal.org/project/context
.. _`Block Visibility Groups`: https://www.drupal.org/project/block_visibility_groups
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
