Enable Blackfire's Continuous profiler [level: Production]
==========================================================

Some extra steps are required to enable the Blackfire continuous profiler to be
added to your application as the feature requires specific libraries
(:doc:`Python </continuous-profiling-cookbooks/python>`,
:doc:`Node.js </continuous-profiling-cookbooks/nodejs>`,
:doc:`Golang </continuous-profiling-cookbooks/go>`,
:doc:`Ruby </continuous-profiling-cookbooks/ruby>`, or
:doc:`Rust </continuous-profiling-cookbooks/rust>`) or a
:doc:`PHP extension </continuous-profiling-cookbooks/php>` as they will be
responsible for collecting the contributions from all the available dimensions
of all functions being executed on all threads at specific intervals.

With the default sampling frequency being ``100 Hz``, this means the continuous
profiler collects information at a rate of 100 times per second.

.. note::

    :doc:`Discover the configuration procedures </continuous-profiling-cookbooks/index>`.
