Understanding Profile Comparison
================================

.. include-twig:: `youtube-iframe`
    :title: Understanding Profile Comparison
    :src: https://www.youtube-nocookie.com/embed/XCft8cHB_0Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we are going to explore one of Blackfire Profiler's most powerful
features: :doc:`comparing two deterministic profiles </profiling-cookbooks/understanding-comparisons>`.

If you ever needed to figure out whether the changes you are about to make to
your application can impact its performance for better or worse, then this one
is for you.

When you are developing a new feature or optimizing existing code, it's essential
to know if your updates have inadvertently affected other parts of your application.

Comparing profile helps you spot unintended side-effects introduced by new code,
validate performance improvements between two versions of the same endpoint, and
prevent regressions by identifying slower function calls right away.

Let's start by accessing your profiles in the Blackfire dashboard.

Once you've run a few deterministic profiles, you will have them listed in your
profile list.

Here is how to compare any two of them. Look for the Compare button on the
right-side of each profile entry. Select a source profile. This might be the
before version. And select a destination profile. The after version you want to
compare against.

Blackfire will then generate a comparison graph that visually highlights the
differences in performance between the two.

Once your comparison is ready, Blackfire displays a superimposed graph merging
old calls from both profiles. You will notice the following: when a function call
or node exists in both profiles, it's displayed as a single node. The node's
background color tells you if the call is faster in profile ``B``, blue, or slower
in profile ``B``, red.

The number at that node represents the performance gain or loss including all
children called within that node.

Sometimes, the paths between shared nodes differ. You might see nodes unique to
profile ``A`` on the left side of the graph, and nodes unique to profile ``B``
on the right side. These single nodes don't have direct counterparts in
other profiles.

As a result, their color coding and displayed numbers are not directly comparable
in the same way as shared nodes.

Performance changes are only meaningful for shared nodes. Because that's where
you have true apples to apples comparison. Here's how the calculation works.

For share nodes, the gain or loss is calculated by subtracting the time or
resource usage of the two nodes. If the graphs diverge between two share nodes,
you can estimate the impact by looking at the first share node before the split
and the next share node after the split. The difference between these two shared
nodes will help you understand the performance impact of that divergent piece of
code.

Here's a quick tip that can help you make effective comparisons. Make sure to
name or label your profiles so you know exactly which version of the code or
environment they belong to.

This will help you organize your comparisons and remember the profile context
when you need it.
