Bitbucket [level: Production]
=============================

`Bitbucket <https://bitbucket.org/>`_ is an Atlassian git product to code,
manage and collaborate. It provides Git repository management, code
reviews, issue tracking, activity feeds, wikis, and continuous integration
features.

Integrating Blackfire with Bitbucket will enable you to automate the performance
testing of your code any time you modify it.

.. caution::

    Note that to do so, you must make sure that any Bitbucket Pull
    Request can be deployed. Blackfire's tests can only be run on a deployed
    environment.

The expected workflow is as follows:

1. A developer in your team creates a Pull Request
2. The Pull Request is automatically deployed
3. Your tooling triggers Blackfire to run your scenarios on the deployed
    environment
4. Blackfire sends a notification to Bitbucket that is displayed as a build
    status on the corresponding Pull Request

.. caution::

    **Please note that only Bitbucket Cloud is supported.**

    Blackfire.io is using the API v2 of Bitbucket for commit statuses and as of
    this writing, Bitbucket Server only supports the v1 API version.

    As an alternative method, we recommend you to use the
    :ref:`webhooks<notification-channel-webhook>` and write a small script
    triggering a commit status using the v1 API (which uses your personal
    credentials).

Start a Build with a Webhook
----------------------------

The first step to configure Blackfire in the above-mentioned workflow is to
create a webhook payload, that Bitbucket will use to let Blackfire run the test
scenarios.

Please read the :ref:`builds webhook documentation<build-webhook>` to configure them.

To make sure that Bitbucket can receive a notification back from
Blackfire, please make sure to configure the following parameters:

======================= =======================
``endpoint``            (Mandatory) The endpoint to profile
``title``               (Optional) Can for instance be the Merge Request reference or title
``external_id``         (Mandatory) The Git commit sha1 related to the build
``external_parent_id``  (Optional) The unique identifier of the parent build
======================= =======================

The `external_id` will make it possible for Blackfire to point the build report
notification to the correct commit. The `external_parent_id` will make it
possible for you to :ref:`write comparison assertions<assertions-comparisons>`.

Setting up the Bitbucket Notification Channel
---------------------------------------------

Anytime a build report is available, the :doc:`Bitbucket notification channel </builds-cookbooks/notification-channels>`
will update the commit status on the corresponding Merge Request.

.. note::

    You must make sure to create the webhook payload like described above.

To configure a Bitbucket notification channel:

* Go to "Bitbucket settings > App password" in Bitbucket to create a new app password,
  and grant it the Repositories ``write`` permissions.
* Go to the Dashboard ``Build`` tab of the related Blackfire environment and look for the
  Notification Channel section.
* Add a new Bitbucket notification channel. The configuration requires the
  repository name (like ``username/project-name``), your Bitbucket username, and
  the Bitbucket app password you have just created to be able to post build
  statuses on merge requests.
