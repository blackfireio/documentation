You should turn on caching for your views in Drupal 8
=====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal 8 uses the Views module to find and display lists of content. A site
may include many different views, displaying different sorts of lists in
different places.

Some views change on every request, for example a list of the most recently
visited pages. Most views, however, only change occasionally. For example, a
list of all articles with a certain tag will only change when an article
is added or edited. The Views module can therefore benefit a lot from caching
the results of a view.

By default, caching is enabled on every view. This caching is safe—views knows
to invalidate the cache when data is edited and the cache is no longer correct.
You should make sure caching is never disabled on views.


How to Enable Caching for a View
--------------------------------

In Drupal, access the **Administration** interface, then click on
Structure > Views to see a list of all the views on your site. Find a view
that has caching disabled, and click the **Edit** button to see the
view configuration page.

Open the **Advanced** section of the view configuration, which may be
collapsed. At the bottom will be a **Caching** setting. Click the link to enter
the Caching dialog. Choose either **Tag based** (to automatically invalidate
the cache based on content being edited) or **Time based** (to invalidate the
cache after a set amount of time). Click **Apply** to exit the Caching dialog,
and then **Save** to save the view.

Repeat this for other views that have caching disabled.

.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
