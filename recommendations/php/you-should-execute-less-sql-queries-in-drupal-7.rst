You should execute less SQL queries in Drupal 7
===============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal stores most of its data in relational databases such as MySQL or
PostgreSQL. It performs many SQL queries to fetch the information needed to
render the contents displayed to the end users.

The vast majority of SQL queries are very fast when executing them in the
database server. However, each SQL query introduces some overhead in your
application. Drupal performs queries mostly synchronously, so each time a
query is sent to the database, your PHP code stops executing and just waits
for a result.

Reducing the Number of SQL Queries
----------------------------------

In Drupal, too many queries is usually a symptom of one of the following other
issues:

* :doc:`Too many separate entity loads </recommendations/php/you-should-load-entities-in-larger-groups-in-drupal-7>`
* :doc:`Too many contrib modules </recommendations/php/you-should-not-use-too-many-contrib-modules-in-drupal-7>`
* :doc:`Disabled caches </recommendations/php/you-should-leave-all-caches-enabled-in-drupal-7>`

You can also see :doc:`generic techniques </recommendations/php/you-should-execute-less-sql-queries>`.

.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
