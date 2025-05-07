Deterministic versus Probabilistic Observability
================================================

.. include-twig:: `youtube-iframe`
    :title: Deterministic versus Probabilistic Observability
    :src: https://www.youtube-nocookie.com/embed/00ZpYkDVfQM?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

:doc:`Continuous profiling </continuous-profiling-cookbooks/index>` is
probabilistic, which differs from our :doc:`deterministic profiling </profiling-cookbooks/index>`,
which is, well, deterministic.

Let's break it down! What's the real difference and why should you care when
improving your app's performance?

The deterministic tools of Blackfire rely on the selection mechanism to target
specific requests or CLI scripts.

You could explicitly ask for a specific request to be profiled using the
:doc:`browser extension </integrations/browsers/index>`.

Blackfire Monitoring uses a :ref:`sampling rate <monitoring_sample_rate>` to
decide whether it should collect information or not.

In all cases, and when a request is selected, our probe start collecting data
from the very first function being called to the very last.

Depending on the case, it'll collect the minimal amount of data for a monitoring
trace, an intermediate amount for the monitoring extended trace and the maximal
amount possible for a full deterministic profile.

The overhead differs for each type of data sample. The larger the sample size,
the higher the overhead.

Continuous profiling relies on a time-based mechanism and collects data at
specific intervals.

When the continuous profiling clock ticks, our probe collects information about
the functions currently being executed on all threads. It gathers its call-stack
and its contribution to the available dimensions .

The data collection process is continuous, hence its name continuous profiling.

Yet the fact that data is actually collected a certain number of times a second,
strongly limits the overhead, making it extremely valuable.

The default sampling frequency is 100 hertz, which means the continuous profiler
probe collects information 100 times per second.

So why is continuous profiling probabilistic? It's because the quality of the
information relies on the quality of the sample.

Depending on your traffic, you might need a large enough sample or timeframe to
get an accurate representation of your real code execution.

Both approaches of their strengths and weaknesses. One is not better than the
other. It all depends on the instrumented languages and your understanding of the data.

For deterministic profiling its strength, lies in precision and facilitating
meticulous script analysis. But it is resource intensive, leading to a
considerable overhead and potential data overload making analysis potentially
tedious.

Probabilistic profiling is lightweight and scalable, tailored for holistic
application oversight. However, its periodic snapshots might miss rapid function
calls yielding a not so perfect application map.

Deterministic and probabilistic profiling each hold value within the development
process.

The former delivers a thorough and detailed view while the latter offers a wider,
more adaptable perspective.

Your next step is now to :doc:`configure continuous profiling <configure>` on
your application.
