Chapter 3 - What is Blackfire?
==============================

Blackfire is a **performance management solution**. The core technology is a
**profiler**, but the product is way more than that. Blackfire fits in your
**development workflow** by providing the following key features:

* A low-overhead profiler that helps developers **debug** performance issues,
  **find** hidden bottlenecks in existing codebases, and **validate** the
  impact of fixes. In production, the profiler helps **diagnose production
  issues**, understand problems, and find solutions fast.

* A platform that stores data history to allow **trend analysis** over time and
  **collaboration** within larger teams.

* Key Integrations with testing libraries, automation software, and
  **continuous integration** and deployment platforms to **automate performance
  testing**, give **fast feedback** to developers, **avoid regressions**, and
  **guarantee** that applications can be deployed with confidence.

Although Blackfire is a unique, integrated performance solution
**for the complete application development lifecycle**, there are other
solutions available that attempt to solve a subset of these problems.
In some cases, these solutions can be used as a complement to Blackfire.

Blackfire vs microtime
----------------------

``microtime()`` is a built-in PHP function and probably the simplest way
to determine how long a snippet of code takes to execute:

.. code-block:: php

    $start = microtime(true);

    // do something

    $stop = microtime(true);
    error_log($stop - start);

Using ``microtime()`` may be easy, but this approach suffers many drawbacks.
First, you must instrument your code manually. How do you know where to start?
Which piece of code do you profile first? It's like shooting in the dark.
What's more, when you end a ``microtime()`` "profiling session", you will have
to go through your code and remove the code you added. And if you want to run a
profile again in the future, you will need to start from scratch.

Using ``microtime()`` for profiling is like using ``var_export()`` or
``echo`` to debug a script when you'd be better off using a tool like Xdebug.
Blackfire automatically instruments your code from inside PHP; there is no
code to add to your project.

Another problem with the ``microtime()`` approach to profiling is that it only
tells you part of the story; the time it takes for a piece of code to
execute tells you nothing about how you can improve your application's
performance.

Perhaps the most significant problem with the simple ``microtime()`` approach
is that it assumes your code executes at the same speed every time and that a
single profile is a reliable measurement of performance. Taking only one
measure is not enough, you need several iterations:

.. code-block:: php

    $start = microtime(true);

    for ($i = 0; $i < 10; $i++) {
        // do something
    }

    $stop = microtime(true);
    error_log(($stop - start) / 10000);

In addition to this average time, you should also calculate the **standard
deviation**. If it is too big, reasoning about the numbers becomes very hard
and often just plain wrong.

Blackfire takes several measurements of the code execution and aggregates
them to get more accurate results. More importantly, time
comes in several flavors. Besides the wall-clock time (what ``microtime()``
returns), Blackfire also gives you the CPU time and the I/O time of
each function call; we will cover this topic in a few chapters but you can
imagine that understanding if your code is I/O bound or CPU bound makes
finding the root cause of a performance problem much easier.

But Blackfire cannot perform miracles and it suffers from the same core
problems when it comes to measuring time; that's why Blackfire also provides
**other dimensions that do not depend on time** and are more stable (like
memory usage, and more specific metrics like the number of executed SQL
queries, web service calls, and more - we will cover those metrics in great
depth in this series).

Blackfire vs Benchmarking Libraries
-----------------------------------

There are many well-established PHP benchmarking libraries available today.
These tools offer a nice alternative to ``microtime()`` and avoid most of the
repetitive, boilerplate code from above, and often include calls to
``memory_get_usage()`` to provide information about memory consumption.
Developers can use these tools to determine which implementation of a given
algorithm is faster.

Benchmarking tools are compelling as they are written in PHP
and don't require a complicated installation. But like pure
``microtime()``, they lack many features needed to seriously manage performance
of large codebases.

When using a benchmarking library, choose one that calculates the standard
deviation and checks that the difference between two algorithm implementations
is **statistically significant**.

Blackfire vs Xhprof
-------------------

Xhprof is one of the oldest pure-profilers in the PHP world. Open sourced by
Facebook in 2009, it provides a low-overhead profiler that you can use on
development machines. Some libraries built on top of Xhprof can also be used
in production, where they will take profiles on a certain percentage of
incoming requests.

Xhprof is provided as a source package, and it's up to you to compile and
install the library, which can be difficult. Furthermore, Xhprof is no
longer maintained by Facebook and the future of the library is uncertain.
Several forks have been created, but as of this writing, support for PHP 7
is still not available.

Blackfire started as a fork of Xhprof, but after some time we decided to start
over from scratch to give ourselves more flexibility, lower the overhead
significantly, and still provide more features.

One of the main differences is that Blackfire automatically instruments
source code without any code changes. Not only does it ease the process,
it also allows Blackfire to gather more information about the runtime
execution (destructors behavior for instance or insights about PHP garbage
collector behavior).

Blackfire is supported, packaged, and maintained for `many different platforms
<https://blackfire.io/docs/up-and-running/installation>`_ and `configuration
management tools <https://blackfire.io/docs/integrations/index>`_.

Xhprof provides a minimal web interface with large tables of numbers and static
image call-graphs that are hard to navigate and most of the time impossible
to generate for larger applications.

Blackfire comes with a modern and fast web interface that lets developers
navigate profiles and call graphs, and works with large codebases.

Being a SaaS product, storage and profile life-cycles are automatically managed
by Blackfire. Also, Blackfire adds a security layer on top of the profiler to
make it convenient and secure to profile projects on production servers and let
large teams collaborate on performance.

Xhprof only provides a profiling tool, and as such, it does not come with any
permanent storage nor management tool for profiles.

Last, but not least, Blackfire does not add any overhead when it is not running
a profile. This is very important for production servers, where Blackfire
only instruments the code when a profile is triggered by an authorized user.

.. _blackfire-vs-newrelic:

Blackfire vs New Relic
----------------------

New Relic is an Application Performance Management (APM) solution. It monitors
mobile and web applications in real-time, enabling developers to diagnose and
fix application performance problems. New Relic supports many languages,
including PHP, and offers some additional features like a server monitoring
service.

New Relic essentially monitors real-user interactions with a website. It
collects data for each request, like the time it takes PHP to generate a
response, SQL queries, HTTP calls, but also some information about browser-side
rendering.

For some requests (key transactions), New Relic gathers more data and provides a
small call graph. As it monitors real-user requests, the instrumentation must
have the smallest overhead possible and the profiling data it provides is less
comprehensive than what full-featured profilers like Blackfire can provide.

Blackfire does not monitor web applications. Its core technology is rooted in
the profiler world. Blackfire never instruments real-user requests.
Instead, authorized users are responsible for triggering
Blackfire manually when a performance issue is detected. Blackfire can also
be run automatically on a pre-defined schedule, or in response to specific
events like when a new version is deployed to production.

Blackfire is useful throughout the application development lifecycle, not just
in production. Using Blackfire, developers can continuously measure and
improve application performance. The best an APM like New Relic can do is alert
you when your production site is slow, which is much too late.
By integrating Blackfire into your development workflow you are helping
developers understand why their code is slowing down earlier in their process,
before these issues reach production.

**Blackfire gives developers the right information at the right moment.**

A unique Blackfire feature is its comparison mode. This helpful call graph view
gives you a visual representation of the impact of your changes and makes it
much easier to validate that a bottleneck has been resolved.

Moreover, modern web stacks rarely consist of just an HTTP endpoint. Most
projects run command-line tools on the server on a regular basis, like
consumers or daemons. Blackfire provides the same set of tools to manage their
performance like the ones available for HTTP requests.

New Relic is a great complement to Blackfire. Whenever it finds a slow page, run
a Blackfire profile to analyze and resolve detected problems.

Blackfire vs Load-Testing Solutions
-----------------------------------

There are many load-testing solutions available on the market, from Open-Source
solutions to hosted server farms able to simulate thousands of simultaneous
users.

Load-testing helps to determine a system's behavior under both normal and peak
load conditions. It helps to identify the maximum number of simultaneous users
an application can accept without too much service degradation. As load-testing
operates at a macro level, hitting an application's entire infrastructure,
it does not give you any information about why you hit a limit and why you
cannot serve more requests per second.

Load-testing solutions are a good complement to Blackfire. You can trigger
some Blackfire profiles on some key HTTP requests while a load-test is in
process to better understand how your code behaves under stress. These profiles
might give you some nice insights about bottlenecks that would be difficult
to spot under normal circumstances.

Blackfire vs JMeter
-------------------

JMeter is an Open-Source software application designed to load-test functional
behavior and measure performance. It simulates a browser by running pre-defined
user scenarios. Like load-testing solutions, it operates at the infrastructure
level.

Scenarios are defined in the JMeter interface, which is very powerful and
allows for great report customization. JMeter supports many protocols, not just
HTTP.

Blackfire offers a similar scenario feature, which lets you simulate complex
user interactions. These scenario reports contain profiles for all executed
HTTP requests and give you detailed insights into what exactly is going on
in your application: the number of SQL queries executed, number of emails sent
synchronously, number of compiled templates, cache usages, ...

One big difference between JMeter and Blackfire is that Blackfire doesn't
load-test the application when running the scenarios like JMeter. It is however
possible to combine JMeter and Blackfire by configuring JMeter to automatically
trigger Blackfire on some requests and generate a nice report about code
behavior under stress.

Blackfire vs Google Chrome
--------------------------

Google Chrome and other browsers offer nice built-in profiling tools. Their
goals are similar to Blackfire's but they operate on the **client-side code**
(JavaScript, DOM rendering, ...) whereas Blackfire operates on the
**server-side code** (PHP).

You should use such tools alongside Blackfire to be able to optimize the
end-to-end performance of your applications as experienced by real users.

Conclusion
----------

Comparing Blackfire with other solutions is a nice way to better understand its
features, but now it's time to test Blackfire on a project and see how it
works. During the next few chapters, we are going to use Blackfire to optimize a
demo application and become more familiar with the main concepts of Blackfire.
