Configuring Blackfire Continuous Profiler for Rust [level: Production]
=======================================================================

.. include-twig:: `youtube-iframe`
    :title: configuring continuous profiling
    :src: https://www.youtube-nocookie.com/embed/1q_E6fk2Q1Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

The Rust continuous profiling is currently made across 3 dimensions:

- **Allocations**: Number of objects allocated

- **Allocated Memory**: Number of bytes allocated

- **CPU**: Time spent running on the CPU

Requirements
------------

- Linux (``glibc`` or ``musl``)

- :doc:`Blackfire Agent </up-and-running/configuration/agent>` >= 2.13.0

Installation
------------

1. Download the latest `ddprof release <https://github.com/DataDog/ddprof/releases>`_.

    .. code-block:: bash
      curl -Lo ddprof https://github.com/DataDog/ddprof/releases/latest/download/ddprof-<ARCH>
      mv ddprof INSTALLATION_TARGET

    ``INSTALLATION_TARGET`` specifies the designated location to store the ddprof
    binary. The examples bellow assume ``INSTALLATION_TARGET`` is set to ``./ddprof``.

   .. include:: _datadog-warning.rst

2. Enable the Rust Continuous Profiler by defining these environment variables:

   - ``DD_PROFILING_ENABLED=true``: controls the activation of the continuous
     profiler.

   - ``DD_SERVICE=my-rust-app``: sets the application name.

   - ``DD_TRACE_AGENT_URL=unix:///var/run/blackfire/agent.sock``: has Blackfire
      Agent collect traces.


3. Modify your service invocation to include the continuous profiler.
   Your usual command is passed as the last arguments to the ``ddprof`` executable.

   .. code-block:: bash

       ./ddprof myrustapp --arg1 --arg2

       # using a shell builtin
       exec ./ddprof myrustapp --arg1 --arg2

There is also some additional configuration that can be done using environment
variables:

- ``BLACKFIRE_LOG_FILE``: Sets the log file. The default is logging to ``stderr``.
- ``BLACKFIRE_LOG_LEVEL``: Sets the log level. The default is logging only errors.
