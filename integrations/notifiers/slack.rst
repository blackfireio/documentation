Slack [level: Production]
=========================

The Slack notification channel posts build reports whenever a build is finished, depending
on its configuration.

To integrate Slack into Blackfire:

1. Follow the Slack guide to `add a webhook integration <https://my.slack.com/services/new/incoming-webhook/>`_;

2. Copy/paste the Webhook URL in the Webhook URL field;

3. Select your Blackfire notifications preferences and click on save.

You can configure when a notification should be posted:

* **On success**: a notification is *always* or *never* sent when the builds
  succeed, or only when the status *changes*;

* **On failure**: a notification is *always* or *never* sent when the builds
  fail, or only when the status *changes*;
