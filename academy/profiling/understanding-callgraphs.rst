Understanding the Call-Graph View
=================================

.. include-twig:: `youtube-iframe`
    :title: Understanding the Call-Graph View
    :src: https://www.youtube-nocookie.com/embed/ZFHSBH0CiYY?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we are going to explore the :doc:`call-graph view </profiling-cookbooks/understanding-call-graphs>`
of the deterministic profile. Understanding the call-graph is essential for
spotting performance bottlenecks and improving your application's efficiency.

Let's start by looking at the three main sections of the Blackfire Profile interface.

First, at the top, we have the toolbar. This control center shows key profile
information and lets you switch between dimensions like wall time, I/O, CPU,
memory, and network usage.

Below is a call-graph, the heart of Blackfire's profile visualization. Think of
it as a roadmap of your code execution, where each node represents a function or
a method.

Finally, on the left, you'll find the function method list, which gives detailed
statistics about each piece of code that was executed.

Now, let's talk about something crucial: **Hot path** or **critical path**.

Do you see these nodes with a colored border in the call graph? Together, they
compose the most resource consuming path for the displayed dimension.

Switching between dimensions, let us discover different call graphs and critical
paths.

Depending on your objective and the problem you're trying to solve, you may want
to favor one over the other.

The call graphs for each dimension use different base colors, but the logic
remains same. The more intense the color, the more resources that section is
consuming.

Don't worry if you have trouble perceiving colors, the shade does not really
matter. Only the color density does.

Now do you see those nodes with a colored background?

These are your application's most active function or service call. And again,
the more intense the color, the more resources that node consumes.

Sometimes, a hot path is perfectly normal, like when processing a large dataset.
But often, it points to a performance bottleneck that needs your attention.

A good practice is to start at the bottom of the critical path, with the critical
nodes. You may be within the dependencies of your application. Then, you start
climbing your call graph up until you reach the point where the function calls
come from your code base.

Now, let's look at how to interpret the numbers. Pay special attention to the
sorting keys at the top of the function list.

Exclusive time, that's how long a function takes to run its own code.

Inclusive time, that's the total time, including waiting for any other functions,
it calls.

Here's a pro tip. Look at the percentages instead of focusing on absolute values.
If a single function is taking up to 40 percent of your total execution time,
that's definitely worth investigating.

Finally, sorting by number of calls can help you identify function calls with
excessive cardinality. That might be a code smell and a sign of mismanaged loops.

Sometimes, you need to dive deeper than just a hot path.

See this magnifying glass icon? Click on it to reveal more nodes that might be
hidden by default.

You can also use the search field to find specific functions you're interested
in and navigate its call stack to understand its context better.

Blackfire intelligently groups what we call proxy nodes. These are intermediate
function calls that might clutter your view.

Don't worry, you're not losing any data. All the nodes are still available in
the function list.

And that's it! You now have the tools to read and understand Blackfire
Deterministic Profile call graphs like a pro.
