You should disable Update manager module in Drupal 8
====================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Smile`_.

The Update manager module periodically checks for new versions of your site's software
(including contributed modules and themes), and alert you to available updates.

The log of available updates will indicate when new releases are ready for download,
and you may configure various options, including frequency of update checking and
notification options (which are performed during cron runs), at the respective module
settings page if you have administration permissions.

Please note that in order to provide this information, anonymous usage statistics
(consisting of a unique key and a list of versions of the software your site is running)
are sent to Drupal.org. If desired, you may disable the Update status module from the
module administration page.

How To Disable Update Manager
-----------------------------

In Drupal, access the **Administration** interface, then
click on Extend > Uninstall module. Check "Update Manager"
and click **Uninstall**.

.. _`Update manager`: https://www.drupal.org/docs/8/core/modules/update/overview
.. _`a contribution by Smile`: https://www.adyax.com/
