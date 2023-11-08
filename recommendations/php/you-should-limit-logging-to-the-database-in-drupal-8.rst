You should limit logging to the Database in Drupal 8
====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

As Drupal runs, it keeps a `log of certain events`_. Here are some examples of
things that are logged:

* Someone tried to access a page they don't have permission to see.
* Someone tried to access a page that doesn't exist.
* A user logged in.
* A node was updated.
* A PHP error or warning occurred, such as accessing an array key that does
  not exist.
* A PHP exception was uncaught.

These logs are useful, but page loads are much faster when they don't have to
write to the database. When something is logged to the database, a database
write occurs, and your performance suffers.


How to prevent database logging
-------------------------------

There are several different approaches, depending on what's being logged:

* **Errors and warnings**: If your code or a module you installed causes PHP
  errors, you can end up with many log entries per page view. Fix your code so
  that it handles problems gracefully.
* **Many unimportant log entries in a single page request**: If your code logs
  information in a loop, and the information isn't critical to have logged,
  change it so that it only logs a summary at the end.
* **Frequent important log entries**: If your code logs a lot of data, and it's
  very important for it to be logged, try logging it to your operating
  system's logging facility. This will reduce load on the database. Follow the
  instructions for the `syslog module`_, including disabling the database
  logging module.
* **Infrequent log entries**: If you only have a few log entries per hour,
  don't worry about it, that's normal.

.. _`log of certain events`: https://www.drupal.org/documentation/modules/dblog
.. _`syslog module`: https://www.drupal.org/documentation/modules/syslog
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal8-recommendations.html
