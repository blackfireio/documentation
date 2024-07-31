Introduction to Profiling
=========================

**Blackfire profiler** measures how executed code consumes resources at runtime
and collects the largest set of multidimensional observability data. Enabling
the comprehensive discovery of performance bottlenecks and understanding of
your code's behavior.

Blackfire profiler for PHP and Python can be used in all environments:
development, test, staging, and production. It requires no code change and
no need to remove instrumentation before releasing to production.

It also has no impact on production for end-users as it only generates overhead
for the developers triggering the profiles.

.. note::

    Blackfire profiler is deterministic, compared to our
    :doc:`continuous profiler </continuous-profiling-cookbooks/index>`,
    which is probabilistic. Check out this `blog post <https://blog.blackfire.io/understanding-continuous-profiling-part-1.html>`_
    to know more about the differences.

Read More on Profiling
----------------------

.. toctree::
    :maxdepth: 1
    :titlesonly:

    index
    triggering-profiles
    timeline
    callgraph
    tips
    recommendations
    addons
    comparison
    distributed-profiling
    assertions
