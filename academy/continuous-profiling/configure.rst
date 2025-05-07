Configure Continuous Profiling
==============================

.. include-twig:: `youtube-iframe`
    :title: Configure Continuous Profiling
    :src: https://www.youtube-nocookie.com/embed/1q_E6fk2Q1Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now, you should be familiar with the concepts behind
:doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`. In today's
video, we explore how to configure it.

As for all of our features, continuous profiling requires a :term:`Probe <Probe>`
and an :doc:`Agent </up-and-running/configuration/agent>` to work.

Blackfire Agent
~~~~~~~~~~~~~~~

The agent is a daemon and an intermediary between the probes and Blackfire
servers, communicating back and forth. All tools use the same agent.

If you have already configured it for Blackfire monitoring or deterministic
profiling, you are okay and can continue with the probe installation. If not,
follow the :doc:`installation instruction </up-and-running/installation>` you'll
is find in our documentation.

Continuous Profiling Probes
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The probes are Blackfire eyes and ears responsible for collecting observability
data from your application while its code is executed. They are specific to
continuous profiling and each run time.

Blackfire utilizes the open source Datadog profiler to collect continuous
profiling traces. The agent sends the data directly to Blackfire's ingesters
where we process and analyze it for your observability needs. On our servers, we
add our secret sauce, transforming raw data into actionable information.

Check the documentation for each runtime. The :doc:`configuration </continuous-profiling-cookbooks/index>`
will be detailed here.

Take note of the environment variables you should configure to ensure continuous
profiling works smoothly.

You should now be able to configure your applications to enable continuous
profiling and start collecting information.

Your next step is to explore the continuous profiling dashboard.
