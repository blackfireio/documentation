The Continuous Profiling Dashboard
==================================

.. include-twig:: `youtube-iframe`
    :title: The Continuous Profiling Dashboard
    :src: https://www.youtube-nocookie.com/embed/-B-9peEP--c?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now you should have the continuous profiling up and running. But how do you
actually read all that data and turn it into answers to your performance questions?

Let's take a tour of the :doc:`Blackfire Continuous Profiling dashboard </continuous-profiling-cookbooks/dashboard>`.

Colors
~~~~~~

The first thing you will notice: colors.

Each color in the flame graph represents a different dimension like CPU-Time,
memory, I/O, or Wall-Time. The more intense the color, the more resources that
function consumes. That makes hotspots ready to spot at a glance.

Don't worry if you have trouble perceiving colors. Their shade don't matter.
Only their density does.

Flame-Graph
~~~~~~~~~~~

Next up: the flame graph itself. Think of it as your application's performance
fingerprint. Each rectangle is a function call.. Wider frames means higher
resource usage. Taller stack mean deeper call chains.

Hover on any frame for details.

Double click to zoom in and navigate through **callers** and **callees**.

Do you prefer raw data over visuals? The **table view** is for you.

Here, every function is listed and sorted by resources consumption.

By default, you will see the exclusive time: the resources spent in that function
alone, excluding its children.

It's perfect to quickly identify your highest resource intensive functions.

Multiple Dimensions and Timeframes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You are not stuck on a single dimension. The dashboard lets you pick any
dimension you want to investigate. The available dimensions differ for each
runtime

And since this is continuous profiling, you can select any timeframe, zoom in on
an incident, or look at longer trends.

Comparison Mode
~~~~~~~~~~~~~~~

Finally, one of the most powerful features: comparison mode.

Pick two timeframes: before or after a deployment, or quiet hours versus peak
traffic.

The continuous profiling dashboard turns raw performance data into clear
insights. It helps you not just find problems, but understand them.
