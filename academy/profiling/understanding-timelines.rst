Understanding the Timeline View
===============================

.. include-twig:: `youtube-iframe`
    :title: Triggering deterministic profiles
    :src: https://www.youtube-nocookie.com/embed/H9RWN9ktiKs?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

Today, we will explore the :doc:`timeline view </profiling-cookbooks/understanding-timelines>`
available in a deterministic profile and learn how to interpret it to identify
application performance issues effectively.

The timeline view is a powerful feature that provides a chronological breakdown
of your application function goals.

It provides a clear visual representation of how different parts of your code
are executed over time.

By showing concurrency or overlaps between processes, it is easier to identify
bottlenecks and see what optimization might be needed.

Here are the key elements you want to focus on. The x axis represents the elapsed
time from the start of the request to the end. Each block corresponds to a
function call. Longer bars means longer execution time.

Hovering over any blocks reveals the full name of the function with its namespace,
eventually the primary metric it contributes to, and its contribution to all
available dimensions.

Clicking on the function call reveals its call stack.

Double click on the function call to zoom in on the related timeframe.

Click and hold on the timeline overview to select a time frame to be displayed.

Some of those blocks or function calls have a colored background.

This means they contribute to some key metrics highlighted at the top of the
metrics list on the left hand side of the timeline view.

Blackfire provides over 400 metrics. Only those related to your application,
runtime, and configuration will be displayed.

Check the documentation under Tests &gt; Metrics, to learn more about creating
your own custom metric to enrich the information you have available using your
own application logic.

Hovering a metric displays a summary of the number of function calls
contributing to it, and their overall contribution to the available dimensions.
This information is useful to provide extra context and can serve as a base when
you will write performance tests.

The threshold timeline metric highlights one or several event blocks in the
timeline view. It is designed to draw your attention to something that Blackfire
considers significant.

The light blue wave in the background represents global memory usage. It
represents the growing peak memory envelope.

A sudden increase can give you a hint on which function calls consume more
memory.

Note that on PHP profiles, the memory graph is always growing as it represents
the peak memory, you can never see it decreasing, even if you manually clear
your application memory.

Finally, you can add markers to your profile timeline view. Markers allows you
to visualize key points you explicitly define in your code. Markers can be
created by adding an instruction in your code, or by defining a custom metric.

Adding these instructions to your code is production safe. When no profile is
requested, this function call operates as a no-op instruction.

The profile timelines view helps you visualize your code execution flow and
quickly identify performance bottlenecks. Combining chronological data with
metrics in sight offers an in depth look at how your application behaves under
real conditions.
