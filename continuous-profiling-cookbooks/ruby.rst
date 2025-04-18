Configuring Blackfire Continuous Profiler for Ruby [level: Production]
=======================================================================

.. include-twig:: `youtube-iframe`
    :title: configuring continuous profiling
    :src: https://www.youtube-nocookie.com/embed/1q_E6fk2Q1Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

The Ruby continuous profiling is currently made across 3 dimensions:

- **CPU Time**: Time spent running on the CPU
- **Wall-time**: elapsed time per function call
- **Allocations**: Number of objects allocated

Requirements
------------

- Ruby >= 2.5
- :doc:`Blackfire Agent </up-and-running/configuration/agent>` >= 2.13.0

Installation
------------

1. Add the ``datadog`` gem to your ``Gemfile`` or ``gems.rb`` file:

   .. code-block:: bash

      gem 'datadog', '~> 2.0'

   .. include:: _datadog-warning.rst

2. Install the gems running the ``bundle install`` command.

3. Enable the Ruby Continuous Profiler by defining these environment variables:

   - ``DD_PROFILING_ENABLED=true``: controls the activation of the continuous
     profiler.

   - ``DD_SERVICE=my-ruby-app``: sets the application name.

   - ``DD_PROFILING_ALLOCATION_ENABLED=true``: enables allocation profiling

   - ``DD_TRACE_AGENT_URL=unix:///var/run/blackfire/agent.sock``: has Blackfire
      Agent collect traces.

4. Add the ``ddprofrb exec`` command to your Ruby application start command:

   .. code-block:: bash

      bundle exec ddprofrb exec ruby myrubyapp.rb

      # Rails example
      bundle exec ddprofrb exec bin/rails s

.. note::

    Alternatively, start the profiler by adding the following code in your
    application's entry point if you can't start it using ``ddprofrb exec``:

    .. code-block:: bash

        require 'datadog/profiling/preload'

There is also some additional configuration that can be done using environment
variables:

- ``BLACKFIRE_LOG_FILE``: Sets the log file. The default is logging to ``stderr``.
- ``BLACKFIRE_LOG_LEVEL``: Sets the log level. The default is logging only errors.
