Writing Assertions
==================

.. include-twig:: `youtube-iframe`
    :title: Writing Assertions
    :src: https://www.youtube-nocookie.com/embed/55McQ8-NAg4?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video, we will explore the power of :doc:`assertions </testing-cookbooks/assertions>`
in Blackfire performance testing.

Assertion lets you set clear performance limits for your application, if the
application goes beyond these limits, the test fails, warning you about
potential issues.

Built-in Metrics
~~~~~~~~~~~~~~~~

Most of what you see in a deterministic profile can be used to create assertions.
This includes metrics like wall-time, I/O, memory usage, network, or all the
metrics listed in the timeline view.

You could find all the :ref:`built-in metrics <metrics-built-in-metrics>` in the
documentation under **Tests** > **Metrics** > :ref:`Built-in metrics <metrics-built-in-metrics>`.
There are over 600 of them already available to you. To write an assertion on a
specific dimension append the dimension name to the metric name separated with a
dot ``.``.

For instance, for the sequel that queries metric, the number of calls is stored
in the ``metrics.sql.queries.count``, and the memory usage in
``metrics.sql.queries.peak_memory``.

To check that you don't have more than 10 SQL queries in an assertion, you will
write ``metrics.sql.queries.count <= 10``.

This opens up immense possibility for your performance test, ensuring you always
have what you need to describe your performance expectations.

Best Practices
~~~~~~~~~~~~~~

Yet we have to be cautious about the assertions we pick. Of course, we want our
applications to be fast. However, it is critical to test the reasons behind your
application speed, not the final response time.

Our advice is always to test the causes and not the outcomes. This leads to more
reliable and secure performance tests.

Ask yourself, what actually makes the script fast? Is it the number of SQL
queries? The number of HTTP requests? How often data is written to the database?
Or maybe a large function that does heavy calculations?

Knowing your application well, helps you identify the right factors to test.

Our next step is to explore the creation of :doc:`custom metrics <custom-metrics>`
based on your own application logic.

Those might be the most efficient and perfectly tailored ones to enforce the
highest performance standards.
