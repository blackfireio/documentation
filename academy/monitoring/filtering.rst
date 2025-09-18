Filtering Transactions
======================

.. include-twig:: `youtube-iframe`
    :title: Filtering Transactions
    :src: https://www.youtube-nocookie.com/embed/pf23gxQuMds?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll explore how to :doc:`filter transactions</monitoring-cookbooks/filtering-transactions>`
in your monitoring dashboard. Filtering helps you focus on what really matters,
whether it's a specific host, method, or runtime, so you can optimize your
application faster and smarter.

Blackfire lets you filter HTTP monitoring data by: ``HTTP host``, ``HTTP method``,
``host`` and ``runtime``.

You can use these filters individually, or combine them for a more targeted view.
For example, you might want to analyze only ``POST`` requests to a specific host,
or exclude a runtime you're not actively monitoring.

Each filter comes with flexible options. You can include specific terms, or
exclude terms you don't want to see.

But that's not all! You can also filter monitoring data by HTTP status or
response time. Here's how. Click on the segment of the graph and Blackfire will
filter data based on that dimension. Want to reset the filter? Click on the graph
again. It's that easy!

Once you've applied filters, the top transaction section updates to show the
most impactful transaction for the selected timeframe. Transactions are sorted
by impact by default, representing the percentage of time processing a specific
transaction compared to all others.

Here is a tip. Start optimizing high impact transactions first. It's the quickest
way to improve overall performance.

You can also sort transactions by numbers of requests, response time, 96th
percentile, memory usage, errors. If you want more details about a transaction,
simply click on its name. This will display all the monitoring data related to it.

Finally, let's look at the transaction breakdown graph. This powerful
visualization shows the evolution of the most impactful transactions over time
for your selected filters.

Focusing on contextualized information helps you understand how your application
dynamics change and where you should direct your optimization efforts.

And that's how you filter transactions in Blackfire Monitoring. By using these
filters, you can quickly identify and prioritize eras for optimization, saving
valuable time and resources.
