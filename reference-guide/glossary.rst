Glossary
========

.. glossary::
  :sorted:

  Call-Graph
    A call-graph is a relational visualization method. Blackfire profiles are
    displayed as call-graphs to show the caller-callee relation between
    the function/method calls, which shows best the code's behavior. It enables for
    instance to understand whether a specific function call is responsible for a
    bottleneck, or if the bottleneck comes from their parents.

  Callee
    A callee is a function/method which is called by another function/method in
    your code.

  Caller
    A caller is a function/method which calls another function/method in your code.

  CPU Time
    The CPU Time is a profiling dimension in Blackfire. It corresponds to the time
    your server's CPU spends executing your code.

  Exclusive Time
    The Exclusive Time is the time spent to execute a function, excluding the
    time spent executing its callees. The exclusive time tells you which
    functions consumed the most time by themselves; those are probably the ones
    you might want to optimize first.

  Extended Trace
    Extended Traces are a small subset of :term:`Monitoring Traces <Trace>`
    for which Blackfire collects more in-depth metrics, such as
    :term:`Spans <Span>`.

  Inclusive Time
    The Inclusive Time is the time spent to execute a function, including all of
    the callees.

  I/O Time
    The I/O time corresponds to the time that the CPU is waiting for input/output
    operations. That can for instance correspond to network (database calls, Redis
    calls, HTTP calls, ...) or disk activity (file inclusions, ...). Keep in mind
    that in Blackfire profiles the I/O is rarely 0 as it also includes
    non-significant activities like memory access.

  Node
    A node is a call-graph element. In Blackfire, it represents a function/method
    call, or an aggregation of calls.

  Organization
    An Organization enables to have multiple projects with different
    subscription levels. They give more flexibility for companies working on
    several projects in parallel to tune the number of users and
    :doc:`environments </reference-guide/environments>` for each project, the
    subscription level, and the billing cycle.

  Percentile
    The value below which a percentage of data falls. Having a 96th percentile
    Response Time of 50ms means that 96% of the transactions have a response
    time below or equal to 50ms.

  Profile
    A profile is the data output while measuring the resource consumption of an
    executed piece of code. In Blackfire, that includes consumption in Wall-time,
    CPU time, I/O time, Memory, Network, HTTP calls, and SQL queries. Profiles are
    the largest level of data collected.

  Pruning
    Part of the data preprocessing done by Blackfire involves removing
    function calls that take less than 1% of the global costs on all
    dimensions (time, CPU, memory, etc.). This is done to reduce the size of the
    profiles and to provide a responsive UI. You won't be able to find these removed
    nodes in the call graph nor in the functions list. Pruning can be disabled
    for :doc:`debugging purposes </profiling-cookbooks/debugging>`.

  Span
    A Span is the representation of a function call over time within Blackfire
    Monitoring. Collecting Spans may generate additional overhead on Extended
    Traces.

  Sub-Profile
    A sub-profile is a regular profile that is linked to the main
    :term:`profile <Profile>` or to one or several other sub-profiles.
    Sub-profiles are part of :ref:`the Distributed Profiling feature <distributed-profiling>`.

  Trace
    Blackfire Monitoring relies on Monitoring Traces, the lightest level of data
    it collects. This is the minimal amount of data gathered for all parts of
    the monitored application and at whichever desired frequency.

  Wall-Time
    The wall time for a function call is the measure of the real time it took to
    execute the code. It’s the difference between the time at which the function
    was entered and the time at which the function was left. It is the sum of
    CPU time + I/O time.
