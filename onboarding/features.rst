Features overview
=================

.. include-twig:: `youtube-iframe`
    :title: introduction-to-blackfire
    :src: https://www.youtube-nocookie.com/embed/vhxi83IOlpo?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

What are the key features and benefits that make Blackfire an essential tool for
developers who want to build resilient, high performance applications?

Application Performance Monitoring (APM)
----------------------------------------

:doc:`Blackfire monitoring </monitoring-cookbooks/index>` provides real time
visibility into your application's behavior and a bird's eye view of one
application's performance for your HTTP and CLI traffics.

Blackfire monitoring lets you know **when and where** a specific issue happened
so you can react quickly.

It allows you to drill down to a specific transaction to explore the different
services contribution to the response time. You then get an in depth understanding
of your system health without needing to rely on guesswork.

Continuous Profiling
--------------------

:doc:`Continuous profiling </continuous-profiling-cookbooks/index>` is a powerful
observability feature that combines profiling and monitoring with minimal overhead.

The continuous profiler periodically captures data at specified intervals. It
gathers information on the functions or services triggered by any active request
or script during those intervals.

By continuously profiling your application, you can easily identify hotspots,
optimize resource usage, and compare timeframes to visually identify the flaky
parts of your application.


Deterministic Profiling
-----------------------

:doc:`Blackfire Profiler </profiling-cookbooks/index>` lets you drill down a
specific part of your application. You locate the exact function or service call
responsible for a performance issue.

Blackfire profiler, lets you understand **why** your application behaves a
certain way.

All your SQL queries and HTTP calls are identified and listed alongside the
:doc:`call-graphs </profiling-cookbooks/understanding-call-graphs>` and
:doc:`timeline </profiling-cookbooks/understanding-timelines>` views.

The profile also provides :doc:`recommendations </testing-cookbooks/recommendations>`,
which are a list of actionable insights, and detailed information about the cache
usage and configuration.

Deterministic profiling for PHP and Python is like having a magnifying glass for
your application. It allows you to drill down into the deepest level of your
code, uncovering inefficiencies, memory leaks, or resource hogging functions.

Alerting
--------

You won't have to sit all day waiting for a crash to happen, you can set up
:doc:`alerts </monitoring-cookbooks/alerting>` to be notified immediately.

You can set up alerts based on custom thresholds for any performance metric that
matters to you. This helps your team take proactive measures before small
performance problems become critical outages.

Alerts and cooldowns escalate to any channel you use, such as email, Slack,
Microsoft Teams, or other web services.

Performance Testing
-------------------

Once a script's code is optimized, one more thing remains before pushing it to
production: **writing tests**.

Blackfire provides an `extensive test suite <https://blog.blackfire.io/getting-started-with-the-blackfire-test-suite-part-1-of-series.html>`_
and integrations with major testing frameworks.

Synthetic Monitoring
--------------------

Last but not least, the performance of your applications' critical user journeys
can also be evaluated regularly. Integrating :doc:`Blackfire builds </builds-cookbooks/index>`
with your CI/CI pipelines prevents a pull request from being merged or code from
being deployed into production if it degrades the performance of your application.

It ensures the performance of your applications in the long run.

Learn more about defining your observability strategy in `this blog post
<https://blog.blackfire.io/blackfire-a-complete-observability-solution.html>`_.
