Magento [language: PHP]
=======================

Adobe Commerce Cloud
--------------------

`Adobe Commerce Cloud <https://magento.com/products/magento-commerce>`_ is
Magento-optimized PaaS (Platform-as-a-Service). It enables to fully automate
continuous integration and continuous deployment of Magento eCommerce websites.

Please follow our documentation for :doc:`installing Blackfire on Adobe Commerce
Cloud </integrations/paas/adobe-commerce-cloud>`.

Validating Code Performance before Merging Changes on Adobe Commerce Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Blackfire can be configured on Adobe Commerce Cloud, to:

* :doc:`Profile Magento shops </profiling-cookbooks/index>` on demand on production,
  staging, integration, and development environments;

* Validate code changes with :doc:`Blackfire builds </builds-cookbooks/index>` at
  each new deployment;

* Enable :doc:`Synthetic User Monitoring </builds-cookbooks/builds-periodic>` and
  proactively identify issues in production.

The following video shows an example workflow when integrating GitHub, Adobe
Commerce Cloud, and Blackfire to automatically check the performance of your
code at each commit.

.. include-twig:: `youtube-iframe`
    :title: magento-integration
    :src: https://www.youtube-nocookie.com/embed/jAFXh7I9Dns?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 560px
    :height: 315px

Magento On Premise
------------------

Magento On Premise installations are all Magento installations that are not on
Adobe Commerce Cloud.

Blackfire works for Magento On Premise just like for any PHP application, and
offers optional Magento-specific :doc:`performance recommendations ("Magento
Add-on") </testing-cookbooks/recommendations>`.

:doc:`Install Blackfire for PHP </install/php>`.

.. _magento-fastly:

Module for integrating Fastly CDN with Magento 2 installations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Blackfire must be able to trigger PHP on the server where you are profiling
(see :ref:`how the Blackfire Stack works <blackfire-stack>`).
To do so, you must make sure that caches are bypassed :ref:`the Blackfire HTTP
headers are preserved <reverse-proxies-headers>`.

* For Adobe Commerce Cloud users, the bypass is configured by default; please
  check with the Adobe Commerce Cloud team if any doubt persists;

* For Magento On Premise users, Fastly created a `module for integrating Fastly
  CDN with Magento 2 installations <https://github.com/fastly/fastly-magento2>`_.
  There is a `specific setting that will activate the bypass in a single click
  <https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-BLACKFIRE-INTEGRATION.md>`_.
