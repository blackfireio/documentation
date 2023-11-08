You Should Use the Syslog Instead of the Dblog Module in Drupal 7
=================================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

For keeping a log of things happening on your website, Drupal uses
the `Watchdog API`_. The watchdog can either be configured to log
to the database using the dblog module or to the file system using
the `syslog`_ module. Both the modules are included in the Drupal 7
core, however, the dblog module is enabled by default.

How To Switch from Dblog to Syslog
----------------------------------

From your site's **Administration** interface, go to the Modules page.
On this page, uncheck the *Database logging* module and check the
*Syslog* module. Once done, click on the *Save configuration* button
at the bottom to make the switch. You can then configure the syslog
module from the *Configuration > Development > Logging and errors* in
your site's administration interface.

.. _`Watchdog API`: https://api.drupal.org/api/drupal/includes%21bootstrap.inc/function/watchdog/7.x
.. _`syslog`: https://www.drupal.org/docs/7/core/modules/syslog/overview
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
