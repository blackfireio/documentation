You should Uninstall Discommended Modules in Drupal 7
=======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal has a `wide ecosystem`_ of contributed modules that can add interesting
and useful features to your site. Some of these modules are strictly for
developers and some others might have security implications if not properly
configured. Ideally, these modules are discommended for production environments
and should be uninstalled on live sites.


Uninstalling Harmful and Unsafe Modules
---------------------------------------

In Drupal, access the **Administration** interface, then click on **Modules**.
Look for the following modules and uncheck the box next to their name to
mark them for disabling.

* Devel
* PHP
* Statistics
* Examples

Click the **Save configuration** button to disable the modules. If a checkbox
is disabled, it means the module is required by another installed module.
The **Description** of the module will list which other modules you would have
to disable first. Once you have disabled these modules, you can uninstall them
by going to the **Modules** page again and visiting the **Uninstall** tab.

You might consider installing the `GOLIVE Checklist`_ and the `Security Review`_
module to see more pre-launch and security tips.

.. _`wide ecosystem`: https://www.drupal.org/project/project_module
.. _`GOLIVE Checklist`: https://www.drupal.org/project/golive
.. _`Security Review`: https://www.drupal.org/project/security_review
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
