Distributed Profiling
=====================

.. include-twig:: `youtube-iframe`
    :title: Distributed Profiling
    :src: https://www.youtube-nocookie.com/embed/YJKq9h9T6bM?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this session, we are going to explore one powerful feature referred by
Blackfire's deterministic profiler: :doc:`distributed profiling </profiling-cookbooks/distributed-profiling>`.

Distributed profiling lets you analyze the performance of multiple services that
interact with your application. This is especially useful if your application
uses multiple microservices or if your main application calls out additional
HTTP  or CLI services.

This feature allows Blackfire to capture performance data, not only from your
primary application,  but also from any downstream services the application calls,
such as microservices.

If those microservices make themselves calls to other HTTP or CLI services, they
will also be profiled. Collecting performance data from all parts of your stack
gives you a holistic view of your entire system, helping you pinpoint bottlenecks
and performance issues.

Enable Distributed Profiling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

How to make it work? The Blackfire probe must be enabled on all services you want
to profile. Blackfire HTTP headers must be preserved between services.
Distributed profiling is automatically enabled by default.

It works across different languages supported by Blackfire Deterministic
Profiling. For example, a CLI Python service can call a PHP based service, and
the performance data will remain associated. .

There is a specific checkbox in the browser extension. The ``--no-propagation``
option does the same when profiling with the CLI.

Behind the Scenes
~~~~~~~~~~~~~~~~~

You might wonder how this operates behind the scenes.

Each profile captured in a service references a parent/child ID to establish its
link.

The probe can automatically handle these profile relationships. Or you can set
them in your code using the Blackfire SDK. Each profile is sent to the agent and
processed independently. Once in Blackfire servers, they are stitched together
into a hierarchy.

Different services can even use different agents in different environments. The
only requirement is that the profiling user has access to these environments.

Experience Distributed Profiling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We designed a simple application for you to experiment with distributed profiling
with `book.b7e.io/cascade <https://www.book.b7e.io/cascade>`_. It makes
recursive HTTP calls.

Using the Blackfire CLI, you can run:

.. code-block:: bash
    :zerocopy:

    blackfire curl -L https://www.book.b7e.io/cascade

You will see how subprofiles are automatically generated for each downstream
call. Note that the first five subprofiles are prioritized with distributed
profiling. If more than five subprofiles exist, they may be throttled.

In the Blackfire UI, the root profile and all subprofiles are grouped together.

This consolidated view shows you all services called, the dependencies and call
hierarchies, a magnifying glass icon next to the caller function name, for
example ``fopen``, that lets you see which part of the code triggered a
sub-request.

All relevant assertions and recommendations are shown in one place.

These holistic perspectives make it easier to spot the exact location of
performance bottlenecks, and whether they occur in the main app or in one of its
dependencies.

Distributed Profiling for HTTP requests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Subprofiles are automatically generated whenever HTTP requests are sent using
cURL or HTTP streams, such as ``fopen`` or ``file_get_contents``.

If you use another method to send HTTP requests, you can still trigger a
subprofile by manually adding the ``X-Blackfire-Query`` header.

Distributed Profiling for CLI scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

And what about distributed profiling with CLI?

If your application spawns child processes, for example, calling CLI commands
from PHP or Python scripts. You can similarly use distributed profiling. Instead
of passing an ``X-Blackfire-Query`` over HTTP headers, set the ``BLACKFIRE_QUERY``
environment variable when you spawn the CLI process. This ensures the subprofile
is linked.

Distributed profiling unveils multiple service architecture performance.
Automatic subprofiles for both HTTP and CLI calls help you understand how each
part of your system behaves under real world loads.

With a clear view of bottlenecks and performance data across multiple services,
you're well on your way to confidently optimizing complex distributed systems.
