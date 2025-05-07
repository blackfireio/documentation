Introduction to Deterministic Profiling
=======================================

.. include-twig:: `youtube-iframe`
    :title: Introduction to Deterministic Profiling
    :src: https://www.youtube-nocookie.com/embed/iCyqQ4spubE?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll introduce Blackfire's :doc:`Deterministic Profiling </profiling-cookbooks/index>`.
By the end of it, you should have the big picture of Blackfire's profiler and
what it can provide you with: detailed multi dimensional insights into your
application's performance to help you uncover those elusive bottlenecks.

Let's start by clarifying what we mean by **deterministic profiling**. In short,
it's the process of gathering performance data in a controlled and on demand way.
Whenever you trigger a profile, Blackfire systematically measures how your code
consumes resources like CPU, memory, and I/O so you can pinpoint exactly where
and why your application might be slow.

Unlike :doc:`Continuous Profiling </continuous-profiling-cookbooks/index>`, which
relies on probabilistic sampling, deterministic profiling captures every function
call during a transaction, giving you the most comprehensive view of your
application's behavior. In a future video, we'll explore the comparisons between
deterministic and continuous profiling.

As a reminder, Blackfire's deterministic stack provides three levels of
performance insights. The simple monitoring traces are high level performance
data samples, collected with nearly zero overhead for your application.
The extended traces provide deeper insights that highlight major calls and SQL
queries and cause light overhead.

The deterministic profiles are the most comprehensive observability data unit
available, detailing the contribution of each function and service calls to all
available dimensions , as as well as information about SQL queries, HTTP requests,
cache usages, and hundreds of metrics. These offer the most extensive data, but
carry the highest overhead.

They are still only triggered when you choose, so end users don't feel any
impact. When you use Blackfire's profiler, you gain a multidimensional
perspective on your code's runtime behavior. It measures how each function calls
consumed resources, collecting large sets of observability data.

Here's a key benefit. You can use Blackfire Profiler across all of your
environments, development, test, staging, and even production, without any code
changes.

No need to modify your application source. No extra instrumentation to remove
before going live. No performance impact on your end users, because overhead is
incurred only when you trigger a profile.

That's it for today's introduction to deterministic profiling with Blackfire.

In the next few videos, we'll explore the many ways of triggering deterministic
profiles, each features of Blackfire deterministic profiling in detail. We will
walk you through analyzing core graphs, timeline view, recommendation and more.
