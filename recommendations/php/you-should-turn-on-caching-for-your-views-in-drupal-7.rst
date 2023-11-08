You should turn on caching for your views in Drupal 7
=====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

One of the most commonly used modules in Drupal 7 is the views module,
used to find and display lists of content. Due to the popularity of this
module, it is included in the Drupal 8 core. A site may include many
different views, displaying different sorts of lists in different places.

Some views change on every request, for example a list of the most recently
visited pages. Most views, however, only change occasionally. For example, a
list of all articles with a certain tag will only change when an article
is added or edited. The Views module can therefore benefit a lot from caching
the results of a view.

In Drupal 7, caching is disabled on most of the views.


How to Enable Caching for a View
--------------------------------

In Drupal, access the **Administration** interface, then click on
Structure > Views to see a list of all the views on your site. Find a view
that has caching disabled, and click the **Edit** button to see the
view configuration page.

Open the **Advanced** section of the view configuration, which may be
collapsed. At the bottom will be a **Caching** setting. Click the link to enter
the Caching dialog. Choose **Time based** (to automatically invalidate
the cache after a certain amount of time has passed) instead of **None**.
Click **Apply** to exit the Caching dialog, and then **Save** to save the view.
Alternatively, you might want to install the `Views Content Cache`_ module
to make a view clear it's cache when certain content is created or updated.

Repeat this for other views that have caching disabled.

.. _`Views Content Cache`: https://www.drupal.org/project/views_content_cache
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
