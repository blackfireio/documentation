Your Observability Strategy
===========================

.. include-twig:: `youtube-iframe`
    :title: Your Observability Strategy
    :src: https://www.youtube-nocookie.com/embed/zibhLfeZnL4?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we dive deep into crafting a custom **observability strategy**
with Blackfire.

By now, you should have a good understanding of what problems Blackfire helps you
solve, and an overview of all Blackfire tools, features, and capabilities.

Now, it's time to strategize.

How do you effectively combine these features to meet your unique goals? Your
strategy will make all the difference whether you're putting out fires in
production or building a solid foundation for the long-term.

The journey to building an effective observability strategy begins with defining
your priorities.

Are you fighting outages and firefighting incidents? Or are you striving for
long-term control and proactive performance optimization? Let's explore these
objectives and how Blackfire can be tailored to meet them at each stage.

Firefighting Mode
~~~~~~~~~~~~~~~~~

If your immediate goal is to fight outages, to keep the application running and
minimize downtime, your focus should be on the features that help you react quickly.

First, start with Blackfire's :doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`.
This feature helps you pinpoint performance bottlenecks in real time, especially
during critical incidents.

By understanding what functions are consuming the most resources, you can
identify problems before they spiral out of control.

Next, leverage  :doc:`Blackfire Monitoring</monitoring-cookbooks/index>` to get a
bird's eye view of your application's activity. Monitoring provides a
comprehensive overview of your application behavior, helping you spot trends and
anomalies.

This high-level visibility lets you quickly identify potential issues and areas
of concern before they escalate.

Finally, use Blackfire :doc:`Deterministic Profiling </profiling-cookbooks/index>`
to identify the root causes of bottlenecks at the function or service call level.

By understanding exactly which part of your code are causing performance issues,
you can make precise optimizations that address the underlying problems effectively.

By combining **continuous profiling**, **monitoring**,and **deterministic profiling**,
Blackfire empowers you to tackle critical performance issues effectively.

It allows you to identify the issue, prioritize their resolution, zoom into your
code until you identify the root cause, and fix the problem. One bottleneck at a
time, you regain control over your application performance.

Proactive Performance Optimization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now, what if you are looking for long-term control and building a culture of
high-quality performance?

The features you focus on will help you prevent issues from arising in the first
place.

First, set up :doc:`real-time alerting </monitoring-cookbooks/alerting>` to ensure
you're the first to be warned of any issues happening to your apps in production.

By defining alert thresholds, you can react promptly to performance problems
before they escalate.

Two. Use the :doc:`Health Report </monitoring-cookbooks/health-report>` to get
an aggregated summary of your application health and performance trends.

This overview helps you monitor your application's overall state and identify
areas that may require attention.

Three. Write :doc:`performance tests </testing-cookbooks/index>` and continuously
extend their coverage to ensure you keep the performance of the most critical
parts of your apps under control.

Regular testing allows you to prevent performance regressions as your
application evolves.

Finally, automate tests with :doc:`synthetic monitoring </builds-cookbooks/index>`.

Integrate synthetic monitoring into your CI/CD pipelines to automate performance
testing. This will futureproof your application and ensure you don't deploy a
version of your app with degraded performance.

Combine strategies
~~~~~~~~~~~~~~~~~~

Of course, these two strategies are not mutually exclusive.

The most effective teams use a combination of these strategies and features
over time to ensure both immediate resilience and lasting control.

For teams that start with firefighting, once the emergencies are under control,
it's critical to move towards proactive testing and long-term planning.
Otherwise, you might face the same issues again and again.

Conversely, teams that start with robust testing and monitoring foundation can
often pivot quickly to handle unexpected incidents thanks to their established
healthy baselines and playbooks.

Building an observability strategy isn't about turning on every feature at once,
it's about knowing where to start based on your needs and gradually expanding your toolset.

Blackfire provides the observability and insights to not only fight today's
fires, but also to build tomorrow's growth.

So what are your objectives today?

Start with the features that align with your goals and grow from there.

We are here to support you, every step of the way.
