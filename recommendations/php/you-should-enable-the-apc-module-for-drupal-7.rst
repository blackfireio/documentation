You should enable APC for Drupal 7
===================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

A Drupal site uses data from many different places: PHP files, INI files,
the database, and more. Reading and processing all those files on every page
load would be very slow. Hence, Drupal keeps it cached in several different
**cache bins**.

These cache bins usually live in the database. But some of them are small
enough that they can be kept in faster RAM instead. If the `APCu PHP
extension`_ is installed along with the `APC module`, Drupal 7 will use
it to make its caches faster.

How To Enable APC
------------------

Most PHP distributions come with this module. You may have to install a
package, eg: ``php-pecl-apcu`` on CentOS or ``php-apc`` on Ubuntu 14.04.
You may also have to enable the module by editing your PHP configuration.
Though APCu is included in Drupal 8 core, for Drupal 7, you can enable it
by installing and enabling the APC module.

.. _`APCu PHP extension`: https://pecl.php.net/package/APCU
.. _`APC module`: https://www.drupal.org/project/apc
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
