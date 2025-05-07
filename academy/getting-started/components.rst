Blackfire's Components
======================

.. include-twig:: `youtube-iframe`
    :title: Blackfire's Components
    :src: https://www.youtube-nocookie.com/embed/G8PQ96EQ5Mw?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll break down the essential components that make Blackfire work,
and what you will need to unleash its potential fully.

Blackfire operates with mostly three key components.

First, **the probes**. They are the eyes and ears of Blackfire, responsible for
collecting observability data from your application while its code is executed.

Then, **the agent**. This is a daemon, an intermediary between the probes and
Blackfire servers, communicating back and forth.

Finally, **Blackfire servers**. They are the brains of the operation, trenching
the collected observability data to provide contextualized information and
actionable insights back to you.

The Probes
~~~~~~~~~~

Let's start with the :term:`probes <Probe>`.

These are lightweight extensions or packages designed for specific runtimes.
Their mission is to watch your code as it executes and collects critical data
about its behavior.

For PHP and Python, probes are vital for the deterministic stack of Blackfire.
This includes **monitoring** and **alerting** for proactive issue detection,
**deterministic profiling** for pinpointing bottlenecks,
the **performance test suites** to assess the performance consequences of
upcoming changes, and **synthetic monitoring** to simulate user journeys.

In short, the deterministic probes enable nearly every Blackfire feature, except
for continuous profiling.

To make triggering deterministic profiling even easier, Blackfire also offers a
:doc:`browser extension </integrations/browsers/index>` for
:doc:`Firefox </integrations/browsers/firefox>` and
:doc:`Chrome </integrations/browsers/chrome>`. This browser extension allows you
to profile your application directly from your browser with just a few clicks.

Now, Blackfire requires separate and specific probes for
:doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`. These are
tailored to capture data at specific intervals. During those intervals, it gathers
information on the functions or services triggered by any active request or script.

Behind the scenes, the continuous profiling probe sends the data they collect to
the same :doc:`Blackfire agent </up-and-running/configuration/agent>`.

The Agent
~~~~~~~~~

Next, let's talk about this agent.

Think of it as the command center orchestrating data flow. It receives the data
collected by the probes. It communicates with Blackfire servers to process and
analyze the data. It receives the :ref:`profile next request <monitoring_profile_next_request>`
and :ref:`automatic profiles <monitoring_automatic_profiling>` orders from
Blackfire servers and transmits them back to the probes.

It also embeds the Blackfire CLI, giving you powerful commands at your fingertips.
The agent relies on specific environment variables to know to which of your
:doc:`Blackfire environments </reference-guide/environments>` send the collected data.

It is recommended that one agent be set up for each application instance. If you
use Blackfire on a containerized cluster, ensure you deploy and configure one
agent per application node or pod.

You should now have a clear understanding on how Blackfire works and the key
components required to fully utilize its capabilities.

Your next step is to follow the installation procedure, ensuring that all
components, probes and agent, and any additional configuration are correctly
installed and set up for optimal performance.
