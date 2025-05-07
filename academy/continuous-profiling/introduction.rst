Introduction to Continuous Profiling
====================================

.. include-twig:: `youtube-iframe`
    :title: Introduction to Continuous Profiling
    :src: https://www.youtube-nocookie.com/embed/uWDdv2IfpXY?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

:doc:`Continuous Profiling </continuous-profiling-cookbooks/index>` is a smart
way to monitor the performance of your app all the time in real conditions.

It means collecting data on how your code behaves while your user are using your
application. From this data, you can find what parts of your code use the most
resources like CPU or memory.

With continuous profiling, you can quickly spot performance issues, understand
them and fix them before they become a real problem.

It is a powerful technique because it's lightweight, scalable, and works
directly in your production environment, giving you holistic application of a
site.

Just like :doc:`Blackfire Monitoring </monitoring-cookbooks/index>`, continuous
profiling needs enough traffic to give you meaningful data.

That's why it's made for production :doc:`environments </reference-guide/environments>`.

In your Blackfire dashboard, the continuous profiling dashboard is available
directly under the continuous profiling tab of your environments.

It lets you visualize the profiling data of a specific application and is
composed of several views: **flame graph**, **table view**, as well as a
**split view**, combining the flame graph and table view.

Each view helps make sense of the profiling data of the selected dimension and
timeframe.

Depending on your programming language, you might see different dimensions to
explore.

As of recording, Blackfire continuous profiling supports :doc:`PHP </continuous-profiling-cookbooks/php>`,
:doc:`Python </continuous-profiling-cookbooks/python>`,
:doc:`Node.js </continuous-profiling-cookbooks/nodejs>`,
:doc:`Go, </continuous-profiling-cookbooks/go>`
:doc:`Ruby </continuous-profiling-cookbooks/ruby>`,
:doc:`Rust </continuous-profiling-cookbooks/rust>`,
and :doc:`Java </continuous-profiling-cookbooks/java>`.

It is the perfect tool to understand what's really happening inside your
decoupled PHP and Python apps to keep them fast and efficient.
