Alerting
========

.. include-twig:: `youtube-iframe`
    :title: Blackfire Alerting
    :src: https://www.youtube-nocookie.com/embed/oMEe6cClgdk?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

Today, let's explore :doc:`Blackfire Alerting </monitoring-cookbooks/alerting>`,
this powerful feature that ensures you're always in the know when your
application behaves abnormally.

Alerting in Blackfire lets you receive notifications whenever we detect abnormal
behavior in your application. These alerts are tailored to your criteria and
business logic.

For example, you can get notified when response times are too slow, or when your
application encounters an unusually high error rate.

With Blackfire, you can configure advanced alerting rules or save time by using
our pre configured templates to get started in minutes. It's all about giving
you flexibility and control.

Let's create an alert rule together.

Start by heading to the Alerting Dashboard and click on the ``Add Alert`` button
on the top right corner. You can also use one of the provided templates by
clicking the arrow next to the button and selecting a template that suits your needs.

Each alert rule includes these key elements:

- a name to identify the rule.
- A metric to monitor.
- threshold that triggers the alert.
- A context for where it applies.
- One or more notification channels to keep you informed.

The metric defines what the alert is monitoring. For instance, you can choose
metrics like ``throughput``, ``response time``, ``memory``, or ``load``.

Metrics also include a value type, such as average, maximum, or specific
percentiles like the 96th percentile. Keep in mind that throughput, meaning your
traffic, doesn't have a value type.

Next, define the threshold for your alert.

The **threshold** determines when the alert will trigger. You will specify a
condition type, like ``is above``, ``is below`` or ``equal``. A threshold value,
the absolute value in your chosen unit.

A **duration**: how long the condition must persist to trigger the alert.

Remember, alarm thresholds always take precedence. For instance, consider a rule
with a warning threshold set at 90 ms and an alarm threshold set at 100 ms.
If the response time hits 120ms, only the alarm will trigger, not the warning.

The context allows you to define where the rule applies, such as web traffic or
CLI processes, like cron jobs or consumers. For more precision, you can use
advanced filtering, leveraging variables like ``transaction name``,
``HTTP response code``, ``HTTP method``, ``host``, or ``hostname``.

Here are some examples:

- Exclude healthchecks transaction, with ``transaction != "health_check"``.
- Monitor only successful responses, with ``code in 200..399``.
- Focus on ``GET`` requests ``method == "GET"``.

These filters use the Symfony expression language, which allows for robust
customization. The related documentation provide a full syntax reference.

Once your alert role is defined, you need to decide how you want to be notified.
Blackfire supports multiple notification channels, including email, Slack,
PagerDuty, AppGenie, and more.

You can add a new notification channel directly from the selection menu,
ensuring alerts reach you whenever you are the most responsive.

For added reliability, you can define escalations, setting additional
notifications if the alert state doesn't change after a defined period.

And to keep track of the past alerts, the alert state history provides a
comprehensive view of the triggered events. Click Show on any rule to review its
history or focus on specific events.

With Blackfire Alerting, you can precisely monitor your applications, ensuring
you're always informed when something needs attention.

Start setting up your alerts rule today and keep your application running at its
best.
