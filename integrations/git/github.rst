GitHub [level: Production]
==========================

`GitHub <https://github.com/>`_ is a Git repository management and hosting
platform for companies, individuals, and Open-Source projects to collaborate,
track bugs, and review code.

Integrating Blackfire with GitHub enables you to automate the performance
testing of your code any time you modify it.

Triggering Scenarios on Deployed Environments
---------------------------------------------

The expected workflow is as follows:

1. A developer in your team creates a Pull Request;

2. The Pull Request is automatically deployed;

3. Your toolchain triggers Blackfire to run your scenarios;

4. Blackfire sends a notification to GitHub that is displayed as a commit
   status on the corresponding Pull Request.

.. caution::

    The following options require that Backfire can reach the HTTP
    server serving the pull request version of the code.

If your toolchain enables you to deploy your code automatically for each new Pull
Request, create a webhook payload that you will use (for instance with Jenkins,
Travis,...) to let Blackfire run the test scenarios.

Please read the :doc:`Synthetic Monitoring documentation
</builds-cookbooks/synthetic-monitoring>` to configure it.

To make sure that GitHub can receive a notification back from Blackfire, please
configure the following parameters:

======================= =======================
``endpoint``            (Mandatory) The endpoint to profile
``title``               (Optional) A title for the build (e.g .the Pull Request reference or title)
``external_id``         (Mandatory) The Git commit hash of the tip of the pull request
``external_parent_id``  (Optional) The Git commit hash of the parent build. This is typically the hash of the pull-request base branch
======================= =======================

The ``external_id`` makes it possible for Blackfire to point the build report
notification to the correct commit. The ``external_parent_id`` makes it possible
for you to :ref:`write comparison assertions <assertions-comparisons>`.

.. note::

    The Git commit hashes passed to ``external_id`` and ``external_parent_id``
    **must not be truncated**.

    Example:

    - Valid commit hash: ``61c9b1b59340c44057635d24fb4d9c05842f4056``
    - Invalid commit hash: ``61c9b1b``

Triggering Scenarios on Non-Deployed Code
-----------------------------------------

Blackfire's PHP SDK enables you to test the performance of your code without
deploying it. You will need to configure it to:

* :ref:`Generate profiles and aggregate them in a build <php-sdk-builds>`;

* :ref:`Send the build result to GitHub as a commit status <php-sdk-commit-status>`.
