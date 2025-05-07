Understanding the Assertions Tab
================================

.. include-twig:: `youtube-iframe`
    :title: Understanding the Assertions Tab
    :src: https://www.youtube-nocookie.com/embed/iCyqQ4spubE?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

By now you should have a solid understanding on how to navigate and interpret the
various sections of your Deterministic Profile UI.

We have explored how to analyze, call graphs and timelines, read function
metrics, and break down performance bottlenecks. In this video, we are focusing
on the final tab in the Deterministic Profile UI: the assertion tab.

Assertions In Blackfire are the result of :doc:`performance tests </testing-cookbooks/index>`.
When you profile your application, whether by sending an HTTP request or
running a CLI command, Blackfire can automatically evaluate a series of tests
you've predefined to keep your application performance in check.

These performance checks can automatically run against the same code you just
profiled, help understand unexpected performance regressions, give you early
warning when an update or code change might degrade performance.

The assertion tabs display all the performance tests or assertions that match the
request or comment you've just profiled. You will see a list of all applicable
tests and whether each test passed or failed, along with any additional insight
into why particular assertion failed.

You can create as many assertions as you need each tailored to measure your
application specific meaningful performance indicators.

Here are some tips:

- First, **focus on causes not consequences**.
  Tests relying on time or memory consumption alone can be volatile, leading to
  false positives or negatives when environmental conditions fluctuate.

  By contrast, test that measures cardinalities, such as the number of SQL
  queries, entities hydrated, or calls to an expensive function, remain reliable
  indicators of deeper performance conditions.

- Second, **write assertions early and often**. Each new feature or major
  refactoring is a chance to add or refine assertions. Use them to set
  expectations for what good performance looks like to you in each part of your
  code base.

- Finally, **automate and integrate with CI/CD**. Make your assertion part of
  your automated pipeline so that any test failures are flagged immediately.
  This ensures performance, doesn't regress and noticed between releases

And that's it for the assertion tab! It's an incredibly powerful tool that
turns performance insight into actionable tests so you can build faster, more
reliable application while catching regression before they become a problem for
your users.

Your next step is to start with performance testing by checking our
:doc:`documentation </testing-cookbooks/index>` or watching the series of videos
dedicated to this subject, which will guide you from your very first test to
their automation using synthetic monitoring and integration with your CI/CD
pipeline.
