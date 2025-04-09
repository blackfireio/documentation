Synthetic Monitoring with Blackfire Builds [level: Production]
==============================================================

.. include-twig:: `youtube-iframe`
    :title: Blackfire Builds 101
    :src: https://www.youtube-nocookie.com/embed/QWTCfvpe3E8?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

:doc:`Periodic builds </builds-cookbooks/index>` constitute a unique
**synthetic monitoring** technique, allowing you to simulate a given set of
actions or paths an end-user would take on your site regularly.

Each scenario step triggering back-end code execution automatically generates a
profile of that code. Each profile is tested against your custom assertions and
:doc:`Blackfire recommendations </testing-cookbooks/recommendations>`.

Builds can be triggered on demand via Blackfire's dashboard or periodically
scheduled every 1, 6, 12, or 24 hours. This allows a periodical check-up on your
application performance and early warning if needed.

Builds can also be triggered via the ``blackfire build-trigger`` command,
via cURL, and even through :doc:`native integrations </builds-cookbooks/builds-integrations>`
with the main CI/CD platforms and PaaS such as :doc:`Platform.sh </integrations/paas/platformsh#builds>`, and :doc:`Upsun </integrations/paas/upsun#builds>`.

You have many options at your disposal to integrate performance tests into your
development and deployment workflow and project the impact of changes before
they reach production.

.. note::

    :doc:`Explore the possibilities </builds-cookbooks/index>`, to schedule
    builds.
