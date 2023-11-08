Scenario Notification Channels [level: Production]
==========================================================

Notification channels are executed whenever a :doc:`scenario </builds-cookbooks/scenarios>` is
finished and a report is available. As notification channels are environment specific,
configure them in the "Notification Channels" section of a "Builds" tab in the dashboard.

Blackfire supports the following notification channels: :ref:`email <notification-channel-email>`,
:ref:`webhook <notification-channel-webhook>`, :ref:`native third party services integrations <notification-channel-native>`.

.. tip::

    If you need different notification channels for your testing, staging, or production
    environments, create several environments with different configurations.

.. _notification-channel-email:

Email [level: Production]
-------------------------

The email notification channel sends emails whenever a build is completed, depending on its
configuration.

First, configure email recipients:

* If you check the "Include environment members", an email will be sent to all members of
  the environment;

* The "emails" input allows you to add emails from people who are not part of
  the environment (or if you want to select only a few people from the environment members).

Then, configure when emails must be sent:

* **On success**: an email is *always* or *never* sent when the builds
  succeed, or only when the status *changes*;

* **On failure**: an email is *always* or *never* sent when the builds fail,
  or only when the status *changes*;

.. note::

    You can create more than one email notification channel if you need to configure
    notifications for different groups of people.

.. _notification-channel-webhook:

Webhook [level: Production]
---------------------------

The most generic notification channel is the **webhook**. Configure a URL on the Environment
notification channels configuration and Blackfire will POST on this URL when a build
starts, progresses, or is completed. The body of each HTTP request is a JSON
payload representing the build.

Here is an example when the build is pending:

.. code-block:: json

    {
        "state": "pending",
        "description": "Profiling... 83%",
        "context": "blackfireio",
        "external_id": "",
        "external_parent_id": "",
        "summary": "",
        "report_web_url": "https://blackfire.io/envs/7ceb6d3d-6bbe-4ae5-9f0a-611474fa543b/builds/23af2ea8-2c84-4366-83bc-6bf25eb4ec77",
        "report_api_url": "https://blackfire.io/api/v2/builds/23af2ea8-2c84-4366-83bc-6bf25eb4ec77"
    }

And one when the build is completed:

.. code-block:: json

    {
        "state": "failure",
        "description": "The Blackfire build failed",
        "context": "blackfireio",
        "external_id": "",
        "external_parent_id": "",
        "summary": "5 failing, 2 successful tests",
        "report_web_url": "https://blackfire.io/build/6f425645-9901-45ad-a4dc-9c2511a3dedf",
        "report_api_url": "https://blackfire.io/api/v1/build/6f425645-9901-45ad-a4dc-9c2511a3dedf"
    }

The ``state`` can have the following values: ``queued``, ``pending``,
``success``, ``failure``, or ``error``.

The ``report_api_url`` and ``report_web_url`` are the URLs where the full
report is available from the API or the web.

.. note::

    You can configure several webhooks if needed.

.. _notification-channel-native:

Native Integrations [level: Production]
---------------------------------------

Blackfire supports several native integrations with third-party tools.
Please check their dedicated documentation:

* :doc:`GitHub </integrations/git/github>`
* :doc:`Bitbucket </integrations/git/bitbucket>`
* :doc:`GitLab </integrations/git/gitlab>`
* :doc:`Slack </integrations/notifiers/slack>`
* :doc:`Pager Duty </integrations/notifiers/pager-duty>`
* :doc:`Opsgenie </integrations/notifiers/opsgenie>`
* :doc:`Microsoft Teams </integrations/notifiers/microsoft-teams>`

