Defining your observability strategy
====================================

The quest for performance is a never-ending journey. It is not won as soon as
that one bottleneck has been patched.

It is an ongoing effort to quickly identify issues and squash them before they
spiral out of control, ultimately keeping performance running as smoothly as
possible in the long term.

The best approach is to come up with a battle plan: your **observability strategy**.

Here are the ways Blackfire's components could be used to craft yours:

Blackfire monitoring
--------------------

:doc:`Blackfire monitoring </monitoring-cookbooks/index>` provides a bird's-eye
view of an application's performance for both HTTP and CLI traffic.

It lets you know when and where a specific issue happened so you can react quickly.

Continuous profiling
--------------------

:doc:`Continuous </continuous-profiling-cookbooks/index>` profiling is a powerful
observability feature that combines profiling and monitoring with minimal overhead.

The continuous profiler periodically captures data at specified intervals. It
gathers information on the functions or services triggered by any active request
or script during those intervals.

Blackfire alerting
------------------

You won't have to sit all day waiting for a crash to happen, you can set up
:doc:`alerts </monitoring-cookbooks/alerting>` to be notified immediately.

Alerts and cooldowns escalate to any channel you use, such as email, Slack,
Microsoft Teams, or other web services.

Blackfire Profiler
------------------

Once a diagnosis is made, you can dig as deep as possible into the application
behavior with :doc:`Blackfire Profiler </profiling-cookbooks/index>` until you
locate the exact function or service calls that are responsible for the
performance issue.

Blackfire Profiler lets you understand why your application behaves a certain way.

Blackfire tests suite
---------------------

Once a script's code is optimized, one more thing remains before pushing it to
production: writing tests.

Blackfire provides an `extensive test suite <https://blog.blackfire.io/getting-started-with-the-blackfire-test-suite-part-1-of-series.html>`_
and integrations with major testing frameworks.

Synthetic monitoring
--------------------

Last but not least, the performance of your applications' critical user journeys
can also be evaluated regularly. Integrating :doc:`Blackfire builds </builds-cookbooks/index>`
with your CI/CI pipelines prevents a pull request from being merged or code from
being deployed into production if it degrades the performance of your application.

Learn more about defining your observability strategy in `this blog post
<https://blog.blackfire.io/blackfire-a-complete-observability-solution.html>`_.
