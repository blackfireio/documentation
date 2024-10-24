GitLab [level: Production]
==========================

`GitLab <https://about.gitlab.com/>`_ is an application to code, test, and
deploy code collaboratively. It provides Git repository management, code
reviews, issue tracking, activity feeds, wikis, and continuous integration
features.

Integrating Blackfire with GitLab enables you to automate the performance
testing of your code any time you modify it.

Triggering Scenarios on Deployed Environments
---------------------------------------------

.. caution::

    The following options require that Backfire can reach the HTTP
    server serving the Merge Request version of the code.

The expected workflow is as follows:

1. A developer in your team creates a Merge Request;

2. The Merge Request is automatically deployed;

3. GitLab triggers Blackfire to run your scenarios;

4. Blackfire sends a notification to GitLab that is displayed as a commit
   status on the corresponding Merge Request.

The first step to configure Blackfire in the above-mentioned workflow is to
create a webhook payload, that GitLab will use to let Blackfire run the test
scenarios.

Please read the :ref:`builds API documentation <build-webhook>` to configure
them.

To make sure that GitLab can receive a notification back from
Blackfire, please make sure to configure the following parameters:

====================== =======================
``endpoint``           *Mandatory* - The endpoint to profile
``title``              *Optional* - Can for instance be the Merge Request reference
                       or title
``external_id``        *Mandatory* - The Git commit sha1 related to the build
``external_parent_id`` *Optional* - The unique identifier of the parent build
====================== =======================

The ``external_id`` makes it possible for Blackfire to point the build report
notification to the correct commit. The ``external_parent_id`` makes it
possible for you to :ref:`write comparison assertions
<assertions-comparisons>`.

Triggering Scenarios on Non-Deployed Code
-----------------------------------------

Blackfire's PHP SDK enables you to test the performance of your code without
deploying it. You will need to configure it to:

* :ref:`Generate profiles and aggregate them in a build <php-sdk-builds>`;

* :ref:`Send the build result to GitLab as a commit status
  <php-sdk-commit-status>`.

Setting up the GitLab Notification Channel
------------------------------------------

Anytime a build report is available, the :doc:`GitLab notification channel
</builds-cookbooks/notification-channels>` updates the commit status on the
corresponding Merge Request.

.. note::
    :class: doc-cta

    You must make sure to create the webhook payload like described above.

To configure a GitLab notification channel, open the dashboard build tab of the
related Blackfire environment and look for the *Notification Channels* section.
Add a new notification channel. The configuration requires the repository
endpoint (like ``https://gitlab.example.com/api/v4/projects/17``) and a GitLab
Token to be able to post build statuses on Merge Requests.
