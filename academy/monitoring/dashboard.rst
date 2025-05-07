Monitoring Dashboard
====================

.. include-twig:: `youtube-iframe`
    :title: Monitoring Dashboard
    :src: https://www.youtube-nocookie.com/embed/le6ayYPO6oM?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll dive into the :doc:`Monitoring dashboard </monitoring-cookbooks/dashboard>`,
your gateway to understanding the health and performance of your applications at
a glance.

The Interactive dashboard lies at the heart of Blackfire Monitoring. It allows
you to filter monitoring data based on ``HTTP host``, ``HTTP method``, ``host``,
and ``runtime``. This flexibility enables you to focus on specific aspects of
your application's performance.

With proper configuration, you can also explore your application CLI activities,
including detailed monitoring of CLI commands, background consumers, and
scheduled CRON jobs.

The dashboard provides key performance metrics that give you a comprehensive
understanding of your applications health.

- **Response time**: quickly see how long it takes for your application to
  process requests.

- **Memory usage**: monitor how efficiently your application is using resources.

- **Request per minute, (RPM)**: keep track of traffic trends in real time.

- **Load and output**: gain insight into the overall demand and effectiveness of
  your application.

One of the most powerful features of Blackfire Monitoring is response time analysis.
It breaks down response time per layer of service, giving you a granular insight
into where time is being spent.

This level of detail helps you pinpoint inefficiencies, whether they stem from
your own code, external services, or on how your application interacts with those
services. It's all about giving you the tools to prioritize optimization effectively.

The monitoring dashboard provides a clear view of the top transactions and service
calls for a selected timeframe. These are sorted by impact, showcasing the
percentage of total processing time each transaction or service consumes compared
to others.

A best practice is to optimize high impact transactions first.

Blackfire Monitoring dashboard doesn't just highlight problems, it helps you
understand the root causes. Whether the issue lies in a third party service,
your application configuration, or the way your app handles external dependencies,
you will have the insight needed to address them before they escalate into user
facing issues.
