Comparing Continuous Profiling Timeframes
=========================================

.. include-twig:: `youtube-iframe`
    :title: Comparing Continuous Profiling Timeframes
    :src: https://www.youtube-nocookie.com/embed/DASuCTt9vHg?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

Did my last deployment really slow things down, or it's just in my head?

How do my applications compare between quiet and rush hours?

With the comparison mode of the Blackfire's :doc:`Continuous Profiling dashboard <dashboard>`,
you don't have to guess.

Performance isn't static. It changes between releases, big traffic or external
factors. Comparing timeframes help you validate improvements, detect regressions
and understand behavior changes.

In the continuous profiling dashboard, toggle the compare button on the top-right
corner.

Select your two timeframes, ``A`` and ``B``. They can overlap or be completely
separate. Your call.

Once enabled, the flame graph shows the difference between ``A`` and ``B``.
Colors tell the story:

- Green means that timeframe ``B`` uses less resources here.
- Red means timeframe ``B`` uses more resources.
- Gray means that node only appeared in one side.

Don't worry if you have trouble perceiving colors. Hovering a span displays a
scale informing you precisely how the resource consumption evolves between the
two samples.

Comparison mode makes it obvious where something changed, but it also helps you
decide what to do next:

- Regression? Optimize or roll back.
- Improvements? Celebrate and share.

Comparing timeframes turns your performance data into real feedback loops.

It is how modern teams catch regression early and keep their applications fast,
stable, and delightful.
