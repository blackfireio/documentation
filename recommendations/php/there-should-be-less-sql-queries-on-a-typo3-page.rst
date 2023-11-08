There should be less SQL queries on a TYPO3 page
================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Susanne Moog`_.

A fully cached TYPO3 page executes about 10 SQL queries on average. You should not need to execute more than 20 even
if your web page is more complicated. Look at ways to cache your content and reduce the overall amount of processing done.

The vast majority of SQL queries are very fast when executing them in the
database server. However, each SQL query introduces some overhead in your
application:

* If the database is located on a separate server, you must take into account
  the round-trip communication needed to send the query and get the results;
* If the database server is under heavy-load, the query execution must wait
  until the server frees some of its resources;
* If your application uses a database abstraction library, such as an ORM, the
  original query must be parsed to get the real SQL query executed and the
  results must be processed to turn them into the structure required by the
  application.

These are some of the reasons why you should not execute too many SQL queries to
generate your contents.

.. _`a contribution by Susanne Moog`: https://blog.blackfire.io/typo3-performance-recommendations.html
