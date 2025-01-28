Configuring Blackfire Continuous Profiler for Java [level: Production]
=======================================================================

The Java continuous profiling is currently made across 3 dimensions:

- **CPU Time**: Time spent running on the CPU
- **Wall-time**: elapsed time per function call
- **Allocations**: Number of objects allocated

Requirements
------------

- Java >= 17
- :doc:`Blackfire Agent </up-and-running/configuration/agent>` >= 2.13.0

Installation
------------

1. Download the latest ddprof Java release:

   .. code-block:: bash

      wget -O dd-java-agent.jar 'https://dtdg.co/latest-java-tracer'

   Alternatively, add the following to your ``Dockerfile`` if you are using Docker:

   .. code-block:: bash

      ADD 'https://dtdg.co/latest-java-tracer' dd-java-agent.jar

   .. include:: _datadog-warning.rst

2. Update your Java application start command:

   .. code-block:: bash

      java \
         -javaagent:dd-java-agent.jar \
         -jar <YOUR_SERVICE>.jar <YOUR_SERVICE_FLAGS>

3. Enable the Java Continuous Profiler by defining these environment variables:

   - ``DD_PROFILING_ENABLED=true``: controls the activation of the continuous
     profiler.

   - ``DD_PROFILING_DDPROF_ENABLED=false``: disables native profiling

   - ``DD_SERVICE=my-java-app``: sets the application name.

   - ``DD_TRACE_AGENT_URL=unix:///var/run/blackfire/agent.sock``: has Blackfire
     Agent collect traces.

   - ``DD_PROFILING_ALLOCATION_ENABLED=true``: enables allocation profiling

   - ``DD_PROFILING_ENABLED_EVENTS="jdk.ObjectAllocationInNewTLAB,jdk.ObjectAllocationOutsideTLAB"``:
     enables Object allocation

There is also some additional configuration that can be done using environment
variables:

- ``BLACKFIRE_LOG_FILE``: Sets the log file. The default is logging to ``stderr``.
- ``BLACKFIRE_LOG_LEVEL``: Sets the log level. The default is logging only errors.
