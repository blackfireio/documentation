Synthetic Monitoring [level: Production]
=========================================

Synthetic monitoring simulates real user journeys against your live
application to verify its performance and behavior.

With :doc:`Blackfire Player </builds-cookbooks/player>`, you write scenarios
in ``.bkf`` files that visit URLs, submit forms, and assert on responses and
performance metrics. Running those scenarios with ``--blackfire-env`` and
``--report`` sends the results to Blackfire and produces a consolidated build
report.

.. code-block:: bash

    blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --report

Player exits with a non-zero code when assertions fail, making it easy to
gate a deployment on performance results. Run it from your CI/CD pipeline
after each deployment, on pull-request preview environments, or on a schedule
— from your own infrastructure, with full control over timing and secret
management.

.. note::

    :doc:`Explore the full setup guide </builds-cookbooks/synthetic-monitoring>`,
    including scenario examples, GitHub Actions integration, pull-request
    comparison builds, and exit-code reference.
