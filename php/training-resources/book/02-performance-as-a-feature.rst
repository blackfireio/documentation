Chapter 2 - Performance as a Feature
====================================

Nobody would ever intentionally deploy a broken application. If your unit tests
are failing, that's a big red flag. However, people deploy applications that are
much slower than their current version every single day. Performance is not seen
as a feature. Requirement specifications go into great detail about end-user
features, design, user experience, etc, but these documents rarely mention the
need for speed.

If your website is broken because of a bug, all developers are going to work
around the clock to fix it as fast as possible. Performance issues should be
receiving the same level of attention, but sadly that's not yet the case. I
think this is because we lack good tools. **You cannot fix something that you
are not aware of**.

However, managing performance is not just about magic tools. **Performance
management is about culture and processes**. But why should you care so much
about performance?

Performance impacts your Business
---------------------------------

Big companies and well-known startups demonstrate over and over again that there
is a direct correlation between the time it takes for an application to respond
and your levels of user engagement, conversions, and ultimately revenue.

Two examples:

1. `Aliexpress <https://edge.akamai.com/ec/us/highlights/keynote-speakers.jsp#edge2016futureofcommercemodal>`_
   reduced load time by 36% and saw a 10.5% increase in orders
   and a 27% increase in conversion for new customers.

2. `Pinterest <https://medium.com/@Pinterest_Engineering/driving-user-growth-with-performance-improvements-cfc50dafadd7>`_
   rebuilt their pages for performance led to a 40 percent decrease in
   wait time, a 15 percent increase in SEO traffic and a 15 percent increase
   in conversion rate to signup.

It's even worse for mobile applications. Optimizing APIs and `UI performance
<https://www.smashingmagazine.com/2015/10/rail-user-centric-model-performance/>`_
is critical for modern mobile applications.

Need some more examples? Here are some conclusions from major players:

* `Google: 2% slower = 2% less searching per user <https://assets.en.oreilly.com/1/event/29/Keynote%20Presentation%202.pdf>`_
* `Yahoo! 400 milliseconds faster = 9% more traffic <https://www.slideshare.net/stoyan/dont-make-me-wait-or-building-highperformance-web-applications>`_
* `AOL: Faster pages = more page views <https://assets.en.oreilly.com/1/event/29/The%20Secret%20Weapons%20of%20the%20AOL%20Optimization%20Team%20Presentation.pdf>`_
* `Shopzilla: 5 seconds faster = 25% more page views, 7 to 12% more revenue <https://conferences.oreilly.com/velocity/velocity2009/public/schedule/detail/7709>`_

Still not convinced? Try your site on `Google's Speed Scorecard <https://www.thinkwithgoogle.com/marketing-strategies/app-and-mobile/mobile-tools-to-optimize-site-and-app/>`_.
Better, if you're working on an eCommerce site, it can also calculate
the revenue impact if you change your site's speed. You'll soon figure out how
fast you can get your return on investment for working on performance!

People don't like to wait when browsing the web or navigating through a mobile
app. 3 seconds of wait is what the average person tolerates nowadays, and that
number is going down every day. Google's recommendation is actually to keep the
server response time below 200ms (time it takes to load the necessary HTML to
begin rendering the page from your server, subtracting out the network latency
between Google and your server).

.. raw:: html

    <blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Adoption of <a href="https://twitter.com/blackfireio">@blackfireio</a> is improving the technical performance, and hence the commercial performance, of our website.</p>&mdash; Sam Burns (@AgileTillIDie) <a href="https://twitter.com/AgileTillIDie/status/647361933566414848">September 25, 2015</a></blockquote>
    <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Measuring Performance
---------------------

What makes our applications slow? What kinds of tools can we use to improve
performance?

Modern cloud platforms sell us infinite resources, which sounds great... but
this is a false promise if you don't also have an infinite budget to match. Most
of us have limited resources at our disposal: CPU time, network, disks, memory,
etc. **Improving performance is all about optimizing resource usage.**

At a macro level, performance depends on a large number of factors including
the time it takes to:

* Generate the page's content on the server (the backend);

* Transmit the data from the server to the client;

* Display the page in the browser (the frontend).

On modern web applications, the lion's share of the time is spent on the
application server and the browser.

Major browsers provide good built-in tools that help you understand how pages
are rendered and `JavaScript executions
<https://developers.google.com/web/tools/chrome-devtools/profile/rendering-tools/js-execution?hl=en>`_.

On the server, most of the time is spent executing the application code you
wrote, which usually includes calls to third-party services like a database
server, a cache system, some external web services, and more. To better
understand **code behavior at runtime**, the **code needs to be instrumented**.
Code instrumentation generates useful data for identifying slow code and
figuring out how to fix it.

Profiling Tools
---------------

Measuring and analyzing the performance of an application is the charge of
**profiling tools**. A profiler instruments the code you want to measure and
generates data about its runtime behavior. It does so by **instrumenting** the
code. Data collected during this process could include:

* The memory consumption;
* The number of times functions are called;
* The duration of functions' execution;
* The number of SQL queries;
* ... and much more.

Be warned that code instrumentation adds some overhead to the runtime execution.
As such, it impacts time measurements. In other words, measuring time takes
time! This is why good profiling tools must have minimal (or at least constant)
overhead to avoid skewing results too much. Keep that in mind when choosing your
tool.

Automation
----------

Using a profiler for ad-hoc analysis is great, but managing performance over
time requires that you continuously check your code's behavior and get immediate
feedback to avoid regressions. The best strategy is to manage performance on a
day-to-day basis during development and testing, but also on your staging and
production servers. Integrating a profiling technology like Blackfire into your
continuous integration/deployment workflow is key to success and one of the main
selling points of Blackfire.

Conclusion
----------

As you might have guessed by now, Blackfire is a profiler, but it is also so
much more. In the next chapter, I will compare Blackfire to other
performance-related solutions to give you a better understanding of what makes
Blackfire unique.
