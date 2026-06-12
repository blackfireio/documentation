Chapter 23 - Continuous Integration
===================================

Continuously deploying code is the holy grail for any project. It starts with
having confidence that changes to be deployed do not contain regressions in
terms of features and performance.

The best way to avoid performance regressions is to integrate Blackfire into
your continuous integration workflow. This chapter describes how you can
achieve that.

Running Scenarios on Every Deployment
-------------------------------------

The easiest way to integrate Blackfire into your continuous integration and
deployment workflow is to run the Blackfire scenarios you have defined in
``.blackfire.yaml`` (or in ``.bkf`` files) each time you deploy your code to
testing, staging, and production.

Run the scenarios with Blackfire Player and add the ``--report`` option to get
an aggregated summary. Player exits with a non-zero code when an assertion
fails, so your pipeline turns red whenever you go over budget:

.. code-block:: bash

    blackfire-player run tests.bkf \
        --blackfire-env=ENV-UUID \
        --endpoint=http://symfony.com/ \
        --report

This works with any tool: integration tools like Jenkins or GitHub Actions, and
deployment tools like Capistrano, Chef, Puppet, or Ansible. Read the
`Synthetic Monitoring documentation
<https://docs.blackfire.io/builds-cookbooks/synthetic-monitoring>`_ for complete
pipeline examples.

Conclusion
----------

Blackfire is not a standalone tool. It integrates seamlessly with the tools you
are already using on a day-to-day basis. Continuous performance management can
be a click of the mouse away.
