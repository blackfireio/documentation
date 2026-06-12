Chapter 16 - Performance Automation
===================================

Do you know why most developers don't manage the performance of their
applications? Many will tell you they don't have the time, but the real reason
is probably that they don't have the right tools. Blackfire fills this gap.
Being able to profile applications in development and diagnose problems in
production is great, but if the process is manual, developers will stop
doing it after a while.

**Automation is key to continuously manage application performance**.

Automation is also key to avoid performance regressions in production.
Blackfire provides a feature that helps developers trigger performance tests on
an application and be alerted whenever a problem occurs.

Writing Scenarios
-----------------

Manually triggering profiles on individual URLs like we did previously works
well on development machines, but it does not scale well for production
monitoring.

Blackfire scenarios let you run a set of profiles on your application's main
URLs or API endpoints. Scenarios are defined in ``.blackfire.yaml`` under the
``scenarios`` section.

Finding Bigfoot scenarios could look like the following:

.. code-block:: yaml

    scenarios: |
        #!blackfire-player
        name "Bigfoot Sightings Scenarios"

        scenario
            visit url("/")
                name "Homepage"

            visit url("/sighting/88")
                name "Sighting #88"

            visit url("/sighting/135")
                name "Sighting #135"

            visit url("/about")
                name "About page"

            visit url("/login")
                name "Login page"

            visit url('/login')
                name 'Failed login attempt'
                method 'POST'
                warmup true

In the example, all scenarios, but the last one, trigger profiles on HTTP
``GET`` requests. For each one of them, Blackfire warms up the URL by hitting
it a few times before generating a profile out of several iterations.

The "Failed login attempt" scenario is more interesting as it requests a
``POST`` request, but a safe one. Without any parameters passed to the request,
we end up in the state after the request is processed.

By default, scenarios for non-GET requests have no warmup and profiles are
generated from only one iteration. But as this "Failed login attempt" is
*idempotent*, the scenario is explicitly configured to enable warmup (``warmup:
true``) for the profile.

.. note::

    Blackfire scenarios have more options as described in the `scenarios
    documentation <https://docs.blackfire.io/builds-cookbooks/scenarios>`_.

Triggering Scenarios
--------------------

Now that the Finding Bigfoot scenarios are defined, we need a way to trigger
them. Blackfire has a straightforward way to run them using `Blackfire
Player <https://docs.blackfire.io/builds-cookbooks/synthetic-monitoring>`_.

.. code-block:: bash
    :zerocopy:

    blackfire-player run monitoring.bkf \
        --blackfire-env=<ENV_NAME_OR_UUID> \
        --report

.. note::

    To use the command above, replace the ``ENV_NAME_OR_UUID`` placeholder with
    the name or UUID of one of your Blackfire environments .

Remember that the main benefits of storing scenarios in a
``.blackfire.yaml`` file alongside your code is to make them specific to
your current work: a pull request, a branch, a specific version of your
code, etc. Whenever you add a new feature, don't forget to update the
scenarios.

Conclusion
----------

In development, update your application scenarios whenever you make significant
changes.

Run the scenarios with Blackfire Player from your CI/CD pipeline on each pull
request, and gate the job on Player's exit code so regressions block the merge.

For production, run Player on a schedule — from a cron job or a scheduled CI/CD
pipeline — to profile your application regularly. See the `Synthetic Monitoring
documentation <https://docs.blackfire.io/builds-cookbooks/synthetic-monitoring>`_
for the full setup.

The SDK is the best way to leverage Blackfire's powerful features, and in the
next chapter we will study some advanced usages.
