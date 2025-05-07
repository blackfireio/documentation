Blackfire's Key Features and Benefits
=====================================

.. include-twig:: `youtube-iframe`
    :title: Blackfire's Key Features and Benefits
    :src: https://www.youtube-nocookie.com/embed/vhxi83IOlpo?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

 In this video, we're going to dive into the key features and benefits that make
Blackfire an essential tool for developers who want to build resilient, high
performance  applications.

By the end of this video, you'll have a clear view of the tools Blackfire
provides you to stay in control of your application performance, whether you're
building new features, preventing bottlenecks or solving unexpected issues.

Continuous observability means that you can understand the behavior of your
application in any environment, whether it's development, staging, or production.
Blackfire helps you continuously monitor and improve your application's
performance by providing actionable insight at every stage.

With end to end visibility, you can identify performance bottlenecks early and
make informed decisions to  enhance  your application's efficiency.

Blackfire Monitoring
~~~~~~~~~~~~~~~~~~~~

The first feature of our continuous observability solution is the application
performance monitoring or APM.

 :doc:`Blackfire Monitoring</monitoring-cookbooks/index>` provides real time
visibility into your application's behavior and a bird's eye view of one
application's performance for your HTTP  and CLI traffics. Blackfire monitoring
lets you know when and where a specific issue happened so you can react quickly.

It allows you to drill down to a specific transaction to explore the different
services contribution to the response time. The result? You get an in depth
understanding of your system health without needing to rely on guesswork. 

Continuous Profiling
~~~~~~~~~~~~~~~~~~~~

Next is Continuous Profiling.

:doc:`Continuous Profiling </continuous-profiling-cookbooks/index>` is a powerful
observability feature that combines profiling and monitoring with minimal overhead.

The continuous profiler periodically captures data at specified intervals.
It gathers information on  the functions or services triggered by any active
request or script during those intervals. By default, the frequency is 100 Hz,
meaning it collects data 100 times per second.

By :doc:`continuously profiling </continuous-profiling-cookbooks/understanding>`
your application, you can easily identify hotspots, optimize resource usage, and
compare timeframes to visually identify the flaky parts of your application.

Continuous profiling is a great way to diagnose performance issues.

Deterministic Profiling
~~~~~~~~~~~~~~~~~~~~~~~

Next up, one of the standout and historical features of Blackfire, the
deterministic, or code level, profiler.

 The :doc:`deterministic profiler </profiling-cookbooks/index>` lets you drill
down a specific part of your application. You locate the exact function or service
call responsible for a performance issue. Blackfire profiler, lets you understand
why your application behaves a certain way.

All your SQL queries and HTTP calls are identified and listed alongside the
:doc:`call-graphs </profiling-cookbooks/understanding-call-graphs>` and
:doc:`timeline views </profiling-cookbooks/understanding-timelines>`. The profile
also provides :doc:`recommendations </testing-cookbooks/recommendations>`, which
are a list of actionable insights, and detailed information about the cache usage
and configuration.

Deterministic profiling for PHP and Python is like having a magnifying glass for
your application. It allows you to drill down into the deepest level of your code,
uncovering inefficiencies, memory leaks, or resource hogging functions.

Alerting
~~~~~~~~

Another key feature is :doc:`real-time alerting </monitoring-cookbooks/alerting>`.

With Blackfire, you can set up alerts based on custom thresholds for any
performance metric that matters to you. This helps your team take proactive
measures before small performance problems become critical outages .

Alerting is built on top of Blackfire Monitoring. You don't have to sit all day
in front of the monitoring, waiting for a crash to happen. You can set  up alerts
and be notified immediately. Alerts and cooldowns escalate to any channel
you use, such as email, Slack, Microsoft Teams, or other web services.

 Once the code of a script is optimized, there is one more thing to do before
pushing to production. And this is writing tests.

Performance Testing
~~~~~~~~~~~~~~~~~~~

Blackfire provides an :doc:`extensive test suite </testing-cookbooks/index>`.
Custom assertions are defined into a .blackfire.yaml file, and they are evaluated
every time a profile is triggered. This eases the detection of performance
regressions.

There are also integrations with :doc:`PHPUnit </php/integrations/phpunit>`,
:doc:`Behat </php/integrations/behat>`,
:doc:`Symfony Functional Tests </php/integrations/symfony/functional-tests>`, and
:doc:`Laravel Tests </php/integrations/laravel/tests>`. Other integrations could
be made thanks to the `PHP SDK </php/integrations/sdk>` and `Python SDK </python/integrations/sdk>`.

Automation
~~~~~~~~~~

The performance of your application's critical user journeys can also be
:doc:`evaluated regularly </builds-cookbooks/index>`. Those user journeys, as
well as the expectations for each of them, can be described in
:doc:`scenarios </builds-cookbooks/scenarios>`.

When evaluating, a profile is triggered at every step of every scenario. As for
profiles, the assertions matching the requests are evaluated and the results are
gathered in what we call a Build report.

A build report is a convenient tool for checking the health of large parts of an
application at once. Blackfire Build can be triggered manually, periodically,
or through webhooks.

 I cannot recommend you enough to plug synthetic monitoring into your
:doc:`CI/CD pipelines </builds-cookbooks/builds-integrations>`. Such integration
prevents a pull request from being merged or code from being deployed into
production if it degrades the performance of your application. It ensures the.
performance of your applications in the long run.

 That's it for our look at the key features and benefits of Blackfire.

One next step is for you to start thinking on how can you assemble those
features to build your own observability strategy.
