Automatic Profiling
===================

.. include-twig:: `youtube-iframe`
    :title: Automatic Profiling
    :src: https://www.youtube-nocookie.com/embed/-1aG-d7O8Vs?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we're exploring one of Blackfire's most powerful features:
:doc:`automatic profiling </monitoring-cookbooks/automatic-profiling>`. This
feature is designed to automatically enrich the insight on your application
performance that are available to you.

Before we dive into automatic profiling, let's quickly recap the three levels of
performance insights the deterministic stack of Blackfire offers.

- First, **simple traces**. Simple traces are high level metrics like overall
  response time and peak memory usage. These come with almost no overhead.

- **Extended traces** provide deeper insights with key metrics, such as
  significant calls and SQL queries.

- **Profiles** are the most detailed view of your application behavior, from
  Wall-time to Memory and SQL queries, all the way to the function call level.
  These provide the richest insights, but come with the highest overhead.

Automatic profiling focuses on collecting profiles automatically, so you can get
fine grained insights without manual effort.

Manual profiling is an essential practice for maintaining optimal performance,
but has limitations. With automatic profiling, Blackfire enhances observability
by automatically capturing a daily snapshot of the 10 most impactful transactions.

It's like having a performance detective working in the background, while you
focus on building fantastic applications.

Here's how automatic profiling works. Blackfire analyzes daily data from your
production environments to identify the 10 most impactful transactions.

This list is based on Blackfire monitoring data, ensuring the most significant
performance outposts are targeted.

The :doc:`Blackfire agent </up-and-running/configuration/agent>` retrieves this
list and shares it with the :term:`Blackfire probe <Probe>`. The probe then
monitors incoming requests and automatically triggers a full profile when a match
is found. One automatic profile is triggered daily for each of the 10 most
impactful transactions.

These profiles are captured on real end-user requests to profile real life context.

Keep in mind that profiles are only generated for programmatically named
transactions. Unnamed or UI- named transaction will not be automatically profiled

For more information, check the documentation on how to name your transactions.

Now a quick note. Profiling does add a small amount of overhead, so it's essential
to use this feature thoughtfully. Automatic profiling triggers just 10 daily
profiles, minimizing the impact while gathering valuable data.

When a profile is generated through automatic profiling, you might notice
something called pre transaction detection in the call graph and timeline.
This happens because Blackfire needs to process part of the request before
deciding whether it should be profiled or not.

The detection phase ensures only the relevant portion of the transaction is
analyzed, leaving the earlier code execution in a pre-transaction detection node.

To recap, automatic profiling helps you identify the most impactful transaction
automatically, gather actionable insights for optimization, save time by
eliminating the need for manual profiling.

Using automatic profiling alongside manual profiling and synthetic monitoring
will allow you to maintain excellent control and insight into your application
performance.
