You should not use too many contrib modules in Drupal 7
=======================================================

.. note::
    :class: recommendation-author-note

    This recommendation is `a contribution by Evolving Web`_.

Drupal has a `wide ecosystem`_ of contributed modules that can add interesting
and useful features to your site. If you need some functionality on your site,
it's often easy to find a module that provides that and add it to your site.

However, each module you add comes with a cost. Each module's ``.module`` file
containing PHP code must be loaded for every single page request. A module can
contain thousands of lines of code, of which you might use only a few lines
for the functionality that matters to you. Nevertheless, the extra code will
still run whenever Drupal invokes the appropriate hooks, which takes time. The
quality of contrib modules varies, and some aren't as efficient as they could
be.

At a certain point, you can end up with `too many modules`_. A good rule of
thumb is that an average site should have fewer than 50 contrib modules. As
you accumulate more modules, they may interact in unexpected ways, making your
site much more complex and slow than it needs to be.


How To Reduce the Number of Contrib Modules
-------------------------------------------

In Drupal, access the **Administration** interface, then click on **Modules**.
Click the checkboxes next to any modules you do not want and then click the
**Save configuration** button. If a checkbox is disabled, it means the module
is required by another installed module. The **Description** of the module
will list which other modules you would have to disable first. Once you have
disabled these modules, you can uninstall them by going to the **Modules** page
again and visiting the **Uninstall** tab.

Here are some guidelines for finding modules to uninstall:

* You may find you're not even using some of the modules that are enabled on
  your site. If you have such unused modules, uninstall them.
* If several modules could accomplish what you need, pick only one. Don't
  keep multiple modules around to do very similar things.
* If you have a choice between several modules, you should usually prefer the
  more popular or smaller one. These will have more attention per line of code,
  and are less likely to have serious bugs or inefficiencies.
* Be willing to trade features for performance. Check each contrib module for
  whether it seems well-written and well-maintained. Does its code
  make sense to you? Is it small enough to comprehend? Are bug reports being
  responded to? If not, perhaps you can live without the feature it
  provides.
* Write your own custom code. If you have giant contrib module for
  one tiny thing, you can often replace it with a minimal amount of custom
  code.


.. _`wide ecosystem`: https://www.drupal.org/project/project_module
.. _`too many modules`: https://www.drupal.org/docs/7/site-building-best-practices/avoiding-too-many-modules
.. _`a contribution by Evolving Web`: https://blog.blackfire.io/drupal-7-recommendations.html
