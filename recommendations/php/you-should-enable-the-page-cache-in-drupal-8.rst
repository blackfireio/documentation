You should enable the page cache in Drupal 8
============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal is a database-driven application which generates contents dynamically.
However, when some page contents don't change frequently and when you have lots
of visitors, generating the same page repeatedly is a waste of server resources.

This problem can be solved with one of the several caches included in Drupal
which is called the **Page Cache**. This cache saves pages when they are first
generated, and serves from the cache in response to future requests.

When enabled, this page cache is only applied to public pages such as your
homepage or node view pages. Private pages such as user accounts or
node edit pages are never cached. Drupal 8 will automatically use the cache
when it's appropriate, and regenerate the page dynamically when it has to.
For example, when a node is edited, a page that displays that node will be
regenerated next time.


How To Enable this Cache
------------------------

In Drupal, access the **Administration** interface,
then click on Configuration > Development > Performance. Make sure the **Page
cache maximum age** is set to a reasonably high value.


Troubleshooting
---------------

Sometimes even when you enable the Page Cache, you may find that your pages are
not being cached. To diagnose this, examine the HTTP response for your page
request. If you see the header ``X-Drupal-Cache: MISS``, that means the Page
Cache is enabled but is not caching the current page.

There are a couple of potential reasons for this:

* Your users have a cookie set. When Drupal sees a cookie, it knows that the
  page may have to be customized, and will not use the Page Cache.

* Your page contains dynamic data, for example: the current time, or the
  current user name. This makes the Page Cache unusable for this page. If the
  page must be extremely fast, you will need to eliminate the dynamic data,
  or fetch it via client-side JavaScript.

  Drupal also has a `Dynamic Page Cache`_ that is a bit slower but allows for
  the page to be cached even though it has personalized data. In this case,
  Drupal only has to render the personalized segments of the page.


.. _`Dynamic Page Cache`: https://www.drupal.org/documentation/modules/dynamic_page_cache
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
