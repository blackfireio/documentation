You should enable CSS aggregation in Drupal 8
=============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

The design of the Drupal interface is created with several CSS stylesheets.
Having the CSS contents scattered across lots of small CSS files is convenient
for designers and developers, but it slows down the web page loading and it
hurts the perceived application performance.

Fortunately, the solution to this issue is very simple: instead of loading lots
of small CSS files, you can combine their contents into a big single CSS file.
Loading one file instead of multiple files makes your web pages load greatly
faster. Drupal will also optimize your CSS files by stripping out comments and
white space.

Drupal includes a feature called **CSS aggregation** which combines all the CSS
files automatically. Make sure that this aggregation of CSS files is enabled.


How To Turn on CSS Aggregation
------------------------------

In Drupal, access the **Administration** interface, then
click on Configuration > Development > Performance. Make sure
**Aggregate CSS files** is checked.


.. _`@import directive`: https://developer.mozilla.org/en/docs/Web/CSS/@import
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
