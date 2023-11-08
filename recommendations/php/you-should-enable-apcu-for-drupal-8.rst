You should enable APCu for Drupal 8
===================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

A Drupal site uses data from many different places: PHP files, YAML files,
the database, and more. Reading and processing all those files on every page
load would be much too slow, so Drupal keeps it cached in several different
**cache bins**.

These cache bins usually live in the database. But some of them are small
enough that they can be kept in faster RAM instead. If the `APCu PHP
extension`_ is installed, Drupal 8 will automatically use it to make its
caches faster.

How To Enable APCu
------------------

Most PHP distributions come with this module. You may have to install a
package, eg: ``php-pecl-apcu`` on CentOS or ``php5-apcu`` on Ubuntu 14.04.
You may also have to enable the module by editing your PHP configuration.

.. _`APCu PHP extension`: https://pecl.php.net/package/APCU
.. _`automatically use it`: https://www.drupal.org/node/2327507
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
