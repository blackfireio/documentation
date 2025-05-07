Introduction to Performance Testing
===================================

.. include-twig:: `youtube-iframe`
    :title: Introduction to Performance Testing
    :src: https://www.youtube-nocookie.com/embed/v7Dy7zMZp9Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

Welcome to this introduction video on :doc:`performance testing </testing-cookbooks/index>`
for :doc:`PHP </php/index>` and :doc:`Python </php/index>`.

We'll show you how Blackfire can help you keep your application fast and efficient.

Performance testing simply means making sure that every part of your application
meets the speed and resource requirements you define.

Blackfire offers a complete set of tools for continuous performance testing,
including a test suite with built-in and custom metrics. With Blackfire, yo
can proactively detect and fix performance bottlenecks before the reach
production and before your users notice them.

Here's how it typically works.

You create or improve a feature in your code. You use
:doc:`Blackfire monitoring </monitoring-cookbooks/index>` or
:doc:`continuous profiling </continuous-profiling-cookbooks/index>` to see which
parts might need optimization. You then use deterministic profiling to understand
your code's behavior.

Once you reach the performance you want, you add performance test to secure your
new version. The place to store this test is a file called ``.blackfire.yaml``.

In that file, you write down what you expect from your scripts or endpoints you
work on.

Every time a profile is triggered either by you manually, by the monitoring,
with the daily automatic profiling of those 10 most impactful transactions, or
by the automatic performance tests, all the assertions matching the profile,
request or script will be automatically evaluated.

If anything doesn't meet your performance standards, you'll know right away so
you can fix it before it becomes a bigger issue.

The more you cover your application with performance tests , the more confident
you can be in its overall performance.

By the end of this video series, you'll know how to write your own performance
tests, set up automatic checks, and make sure every new features meets your
performance standards.

Your next step is to write your first performance test.
