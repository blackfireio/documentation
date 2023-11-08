Microsoft Teams [level: Production]
===================================

The Microsoft Teams notification channel posts build reports whenever a build is
finished, depending on its configuration.

To integrate Microsoft Teams into Blackfire:

1. Follow the Microsoft Teams guide to `add a webhook connector <https://msdn.microsoft.com/en-us/microsoft-teams/connectors>`_;

2. Copy/paste the Webhook URL in the Webhook URL field;

3. Select your Blackfire notifications preferences and click on save.

.. note::

    You can use the following `icon <https://blackfire.io/blackfire.png>`_.

You can configure when a notification should be posted:

* **On success**: a notification is *always* or *never* sent when the builds
  succeed, or only when the status *changes*;

* **On failure**: a notification is *always* or *never* sent when the builds
  fail, or only when the status *changes*;
