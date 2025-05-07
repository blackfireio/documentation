Configuring Blackfire Monitoring
================================

.. include-twig:: `youtube-iframe`
    :title: Configuring Blackfire Monitoring
    :src: https://www.youtube-nocookie.com/embed/XKxe6NkJrYg?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll explore how to :doc:`configure Blackfire monitoring </monitoring-cookbooks/configuration>`.
By the end of this video, you should know how to activate monitoring in your
environment and configure key settings such as sample rates.

To get started, you need to be either a manager of your environment or an
organization admin. If you are an organization admin, you can go to your
organization menu from the Blackfire dashboard and click organization
monitoring usage, then simply click enable.

At the environment level monitoring can be controlled from the monitoring
settings of your environment settings. You will also find a graph of the
monitoring usage for that environment.

Good news Blackfire monitoring is enabled by default on the recent PHP and
Python probes. If you are running an older version, or if you previously
explicitly disabled it, you can easily enable it again with these steps.

Alternatively, you can rely on the ``BLACKFIRE_APM_ENABLED`` environment variable
to control the status of that feature. You will find all the environment variables in the documentation under :doc:`PHP > Configuration </php/configuration>` and
:doc:`Python > configuration </python/configuration>`.

Clicking the ``Edit monitoring settings`` button allows you to
:ref:`control the sampling rates <monitoring_sample_rate>`. The sample rate
determines the percentage of requests Blackfire will monitor. Each monitored
request generates a trace, which provides general performance metrics with
virtually no overhead

You can adjust your sample rate to balance cost and visibility. With a higher
trace quota, you can comfortably increase your sample rate to capture more
real-world requests.

Note that lowering your sample rate might help you control your costs, but will
reduce the quality of the observability information at your disposal.

Now, let's talk about the extended sample rate, which controls how many of
those traces are collecting using even more in depth metrics.

These are called extended traces.

In Extended Traces, you will see spans, which represent function calls over
time, similar to what you see in a profiling timeline.

This extra detail is incredibly helpful if you want to pinpoint issues in
real-world contexts. Remember, it adds some overhead, so choose an extended
sample rate that balances depth and performance impact. The default value is 1%.

We've covered how to activate Blackfire Monitoring, adjust your sample rate and
extended sample rate.

With these settings in place, you'll gain continuous observability over your
applications, helping you make informed decisions about performance optimizations.
