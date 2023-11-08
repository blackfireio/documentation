You should enable JavaScript aggregation in Drupal 7
====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

The dynamic features of the Drupal interface are created with several
JavaScript files. Having the JavaScript code scattered across lots of small
JavaScript files is convenient for developers, but it slows down the web page
loading and it hurts the perceived application performance.

Fortunately, the solution to this issue is very simple: instead of loading lots
of small JavaScript files, you can combine their contents into a big single
JavaScript file. Although the amount of data transferred is the same, loading
one file instead of multiple files makes your web pages load greatly faster.

Drupal includes a feature called **JavaScript Aggregation** which combines all
the JavaScript files automatically. Make sure that this aggregation of
JavaScript files is enabled.


How To Turn on JS Aggregation
-----------------------------

In Drupal, access the **Administration** interface, then
click on Configuration > Development > Performance. Make sure
**Aggregate JS files** is checked.

You can also install a module such as `Advanced CSS/JS Aggregation`_ to
further optimize your JavaScript files by minimizing the size of each file.

.. _`Advanced CSS/JS Aggregation`: https://www.drupal.org/project/advagg
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
