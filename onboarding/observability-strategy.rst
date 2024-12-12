Defining your Observability Strategy
====================================

.. include-twig:: `youtube-iframe`
    :title: introduction-to-blackfire
    :src: https://www.youtube-nocookie.com/embed/zibhLfeZnL4?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

The quest for performance is a never-ending journey. It is not won as soon as
that one bottleneck has been patched.

It is an ongoing effort to quickly identify issues and squash them before they
spiral out of control, ultimately keeping performance running as smoothly as
possible in the long term.

The best approach is to come up with a battle plan: your **observability strategy**.

An effective observability strategy involves combining features in a way that
aligns with your unique goals. Whether you are responding to production issues
or striving to build a solid, long-term foundation for performance, your
strategy will make all the difference.

Defining your Priorities
------------------------

Your observability strategy starts by defining your priorities.

Are you currently dealing with outages and firefighting incidents? Or are you
focused on long-term performance and proactive optimization?

This guide will help you tailor Blackfire to meet your needs at each stage.

1. Fighting Outages and Incident Response
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If your immediate goal is to minimize downtime and keep your application running
smoothly, focus on features that help you react quickly:

- **Continuous Profiling**:
  Use Blackfire's :doc:`continuous profiling </continuous-profiling-cookbooks/index>`
  to identify performance bottlenecks in real time. It helps pinpoint which
  functions are consuming the most resources, allowing you to address issues
  before they escalate.

- **Monitoring**:
  :doc:`Blackfire monitoring </monitoring-cookbooks/index>` provides a
  bird's-eye view of your application's behavior, highlighting trends and
  anomalies. This high-level visibility helps you spot potential issues before
  they become critical.

- **Deterministic Profiling**:
  For precise optimizations, use Blackfire's
  :doc:`deterministic profiling </profiling-cookbooks/index>` to identify root
  causes at the function or service call level, ensuring that you can
  effectively address underlying problems.

By combining these features, you can efficiently tackle critical performance
issues, regain control over your application's performance, and resolve
bottlenecks one at a time.

2. Long-term Control and Proactive Optimization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you're focused on building a culture of high-quality performance and
preventing issues from arising, focus on the following features:

- **Alerting**:
  Set up :doc:`alerting </monitoring-cookbooks/alerting>` to ensure you are
  the first to know about any production issues. By defining alert thresholds,
  you can respond to performance problems promptly.

- **Health Report**:
  Use :doc:`Health report </monitoring-cookbooks/health-report>`
  to get an aggregated summary of your application's health and performance trends.
  This helps you monitor the overall state and identify areas needing attention.

- **Performance Testing**:
  Write and continuously expand
  :doc:`performance tests </testing-cookbooks/index>` to keep critical parts of
  your application under control. Regular testing prevents performance
  regressions as your application evolves.

- **Synthetic Monitoring**:
  Automate performance test with :doc:`synthetic monitoring </builds-cookbooks/index>`
  by integrating it into your CI/CD pipeline. This ensures your application
  maintains performance quality with each new release.

Combining Strategies for Effective Observability
------------------------------------------------

These strategies are not mutually exclusive. The most successful teams combine
both approaches to achieve immediate resilience and lasting control.

For teams starting with firefighting, it is essential to move toward proactive
testing and planning once emergencies are under control. Otherwise, recurring
issues will keep reappearing.

Teams that start with a strong foundation of testing and monitoring can often
handle unexpected incidents more effectively due to established healthy
baselines and clear playbooks.

Building an observability strategy with Blackfire isn't about enabling every
feature at once. Instead, start by focusing on your current needs and gradually
expand your toolset as your application matures.

Blackfire equips you with the insights to fight today's fires and build
tomorrow's growth. Define your objectives, start with the features that align
with those goals, and grow your strategy over time.
