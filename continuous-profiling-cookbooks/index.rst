Continuous Profiling Cookbooks [level: Production]
==================================================

.. include-twig:: `youtube-iframe`
    :title: what-is-continuous-profiling
    :src: https://www.youtube-nocookie.com/embed/uWDdv2IfpXY?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Continuous profiling is a multi-dimensional performance optimization technique
where web applications are monitored and profiled in real-time. Lightweight and
scalable, it's tailored for holistic application oversight.

Continuous profiling collects performance data continuously, enabling developers
to gain deep insights into their application's behavior, identify bottlenecks,
and optimize code for better performance and resource utilization. This proactive
approach allows for quicker identification and resolution of performance issues,
ensuring the smooth running of software in live environments.

Continuous profiling on Blackfire
---------------------------------

The continuous profiling dashboard is available directly under the
``Continuous Profiling`` tab of your environments.

It lets you visualize the profiling data of a specific application and is
composed of several views: flame graph, table view, as well as a split view
combining the flame graph and table views.

Each view helps make sense of the profiling data for the selected dimension and
time frame. The available dimensions vary with the runtime profiled.

Read More on Continuous Profiling
----------------------------------

.. toctree::
    :maxdepth: 2
    :titlesonly:

    Deterministic vs probabilistic profiling <understanding>
    PHP configuration <php>
    Python configuration <python>
    Go configuration <go>
    Java configuration <java>
    Ruby configuration <ruby>
    Rust configuration <rust>
    Node.js <nodejs/index>
    Dashboard <dashboard>
    Comparing timeframes <comparison>
