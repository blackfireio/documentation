You should turn off automated cron in Drupal 7
==============================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal requires some maintenance tasks to run periodically such as cleaning
up log files or checking for updates. By default, Drupal 7 checks
cron settings at the end of each request to see if these tasks need to be run,
and if so it runs them.

This is fully automatic, requiring no setup. However, it means the cost of
running these tasks will be added on to an arbitrary request, slowing down
the experience for a user.

It's better to use an external way of running tasks periodically, which is
both more reliable and won't impact random users.


How to Turn Off Automated Cron
------------------------------

First, you will need to setup an external service to trigger Drupal's
periodic tasks. The most common way to do this is by `configuring the Unix
cron command`_.

Once that is done, you can turn off Automated Cron. In Drupal, access the
**Administration** interface, then click on Configuration > System >
Cron. Make sure the **Run cron every** setting is set to **Never**.

.. _`configuring the Unix cron command`: https://www.drupal.org/node/23714
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html

