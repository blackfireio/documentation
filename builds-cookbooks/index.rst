Using Builds [level: Production]
================================

.. include-twig:: `youtube-iframe`
    :title: Blackfire Builds 101
    :src: https://www.youtube-nocookie.com/embed/QWTCfvpe3E8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Blackfire Builds offer various options to automatically profile your code, and
to :doc:`run assertions </testing-cookbooks/assertions>` against it.

A Build is a collection of profiles, resulting from :doc:`scenarios
</builds-cookbooks/scenarios>` which are triggered upon an event.

Build Statuses
--------------

When complete, Builds have a status (Successful, Failed or Errored).

The Successful and Failed statuses depend on the :doc:`assertions
</testing-cookbooks/assertions>` which you write. If you don't write any
assertion, Blackfire may still mark the Build as Failed if a
:doc:`recommendation </testing-cookbooks/recommendations>` is detected.

Builds are Errored when your scenarios cannot be completely executed. This
may happen either when something is going wrong with your Builds configuration, or
when a :ref:`Blackfire Player expectation <writing-expectations>` fails.

Triggering a Build
------------------

Builds can be triggered with:

* functional tests in a CI/CD pipeline (e.g. with our :doc:`CI/CD third party
  integrations </integrations/ci/index>`, :doc:`Behat </php/integrations/behat>`,
  :doc:`PHPUnit</php/integrations/phpunit>` or :doc:`Symfony Function Tests
  integration </php/integrations/symfony/functional-tests>`);

* :ref:`synthetic monitoring <trigger-scheduled>` on production or staging;

* :ref:`deployments via integrated PaaS services <build-integrations>`;

* :ref:`custom integrations <build-webhook>`;

* custom scripts with our :doc:`PHP SDK </php/integrations/sdk>` and :doc:`Python
  SDK </python/integrations/sdk>`;

* :doc:`Blackfire Player </builds-cookbooks/player>` scripts.

.. caution::

  In most cases, Builds are run from the Blackfire's servers.
  As a result, if the profiled application is behind a firewall, you must
  let the Blackfire servers access the application by **allowing the following
  IP addresses** on the web ports (usually ``80`` and ``443``):

  * ``46.51.168.2``
  * ``54.75.240.245``

Being Notified of a Build Report
--------------------------------

When a Build is complete, you may receive :doc:`notifications
</builds-cookbooks/notification-channels>` where and when it matters to you.

Read More on Builds
-------------------

.. toctree::
    :maxdepth: 2
    :titlesonly:

    scenarios
    player
    builds-periodic
    builds-webhook
    builds-integrations
    notification-channels
