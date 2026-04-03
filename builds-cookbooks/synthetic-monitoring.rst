Setting up Synthetic Monitoring [level: Production]
===================================================

.. _synthetic-monitoring-player:

Synthetic monitoring simulates real user journeys against a live application
to verify its performance and behavior. With
:doc:`Blackfire Player </builds-cookbooks/player>`, you control when and where
these scenarios run: from your CI/CD pipeline after a deployment, on pull
requests, or on your own schedule.

Why run synthetic monitoring from your pipeline
-----------------------------------------------

Running synthetic monitoring from your own infrastructure offers key
advantages over external scheduling:

* **Works behind firewalls and VPNs.** Because Player runs from your
  environment, the profiled application need not be publicly accessible.

* **Runs exactly when you need it.** Trigger monitoring on every deployment,
  on pull requests, or on demand — without an external scheduler.

* **Integrates natively with your pipeline.** Exit codes let you gate
  deployments on assertion results.

* **Targets any environment.** Point Player at feature-branch previews,
  staging, or production using ``--endpoint``.

* **Gives you a consolidated report.** The ``--report`` flag produces
  an aggregated summary with links to each profile. Results are also
  sent to your Blackfire environment for history, notifications, and
  comparison.

Prerequisites
-------------

* :doc:`Blackfire Player </builds-cookbooks/player>` available in your
  environment (Docker image ``blackfire/player``).

* Your :ref:`Blackfire client credentials <cli-client-env-vars>`:
  ``BLACKFIRE_CLIENT_ID`` and ``BLACKFIRE_CLIENT_TOKEN``.

* A Blackfire :doc:`environment </reference-guide/environments>` UUID or name
  to send profiles to.

Writing monitoring scenarios
----------------------------

Write your scenarios in a ``.bkf`` file, covering the critical user journeys
you want to monitor: key pages, authentication flows, checkout paths, API
endpoints.

Add :doc:`Blackfire assertions </testing-cookbooks/assertions>` on each step
to enforce your performance budget:

.. code-block:: blackfire

    name "Synthetic monitoring"
    endpoint "https://example.com"

    scenario
        name "Homepage"

        visit url('/')
            name "Homepage"
            expect status_code() == 200
            assert main.wall_time < 500ms
            assert metrics.sql.queries.count < 10

    scenario
        name "Product catalog"

        visit url('/products/')
            name "Product listing"
            expect status_code() == 200
            assert main.peak_memory < 50mb

        visit url('/products/featured/')
            name "Featured products"
            expect status_code() == 200
            assert main.wall_time < 300ms

.. tip::

    Without assertions, Blackfire still evaluates its built-in
    :doc:`recommendations </testing-cookbooks/recommendations>` against each
    profile, providing a useful baseline.

Running synthetic monitoring
----------------------------

Use ``--blackfire-env`` to associate profiles with your Blackfire environment,
and ``--report`` to print an aggregated summary:

.. code-block:: bash

    blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --report

The ``--report`` flag prints a summary after all scenarios complete, listing
each step with a link to its profile and key performance figures.

To target a different endpoint — a freshly-deployed environment, for example
— use ``--endpoint``:

.. code-block:: bash

    blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --endpoint=https://staging.example.com \
        --report

``blackfire-player run`` exits with a non-zero code when assertions fail,
letting you gate the CI job accordingly:

* ``64`` — at least one scenario fails;
* ``65`` — a fatal error prevents scenarios from running;
* ``66`` — a non-fatal error occurs.

Integrating with CI/CD pipelines
---------------------------------

Post-deployment verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run Player after each deployment to staging or production; the pipeline fails
automatically if assertions do not pass.

**GitHub Actions example:**

.. code-block:: yaml

    - name: Run synthetic monitoring
      env:
        BLACKFIRE_CLIENT_ID: ${{ secrets.BLACKFIRE_CLIENT_ID }}
        BLACKFIRE_CLIENT_TOKEN: ${{ secrets.BLACKFIRE_CLIENT_TOKEN }}
      run: |
        docker run --rm \
          -e BLACKFIRE_CLIENT_ID \
          -e BLACKFIRE_CLIENT_TOKEN \
          -v "$(pwd):/app" \
          blackfire/player run monitoring.bkf \
            --blackfire-env=${{ vars.BLACKFIRE_ENV_UUID }} \
            --endpoint=${{ vars.STAGING_URL }} \
            --report

Pull-request performance checks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run Player against a pull request's preview environment to catch regressions
before merge. Use :ref:`build comparison assertions <builds-comparison-player>`
to assert metrics do not degrade relative to a reference build:

.. code-block:: bash

    BLACKFIRE_EXTERNAL_ID=$PR_SHA \
    BLACKFIRE_EXTERNAL_PARENT_ID=$BASE_SHA \
    blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --endpoint=https://preview-$PR_NUMBER.example.com \
        --report

Scheduled monitoring
~~~~~~~~~~~~~~~~~~~~~

Run Player on a schedule using cron or a CI/CD scheduled pipeline. This
gives you full control over frequency and target environment, as an
alternative to :doc:`Blackfire's server-side periodic builds
</builds-cookbooks/builds-periodic>`:

.. code-block:: bash

    0 * * * * cd /path/to/project && \
      blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --report >> /var/log/blackfire-monitoring.log 2>&1
