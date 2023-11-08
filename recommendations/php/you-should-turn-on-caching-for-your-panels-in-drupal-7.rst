You should turn on caching for your panels in Drupal 7
======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

The `Panels`_ module allows a site administrator to create customized
layouts for multiple uses. At its core it is a drag and drop content
manager that lets you visually design a layout and place content within
that layout.

When used along with the *Page Manager* modules (part of the `ctools`_)
module, panels lets the administrator create dynamic pages with various
customized layouts.


How to Enable Caching for a Panel
---------------------------------

In Drupal, access the **Administration** interface, then click on
Structure > Pages to see a list of panels on your site. Find a panel
that has caching disabled, and click the **Edit** button to see the
panel configuration page.

In the panel configuration, go to the **Content** sub-tab and near
the top of the pane, click the **Display Settings** link. You will
see a popup menu with an option to **change** the caching settings.
Once done, make sure you save the panel settings.

Repeat this for other panels that have caching disabled.

.. _`Panels`: https://www.drupal.org/project/panels
.. _`ctools`: https://www.drupal.org/project/ctools
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
