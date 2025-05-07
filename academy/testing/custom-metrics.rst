Writing Custom Metrics
======================

.. include-twig:: `youtube-iframe`
    :title: Writing Custom Metrics
    :src: https://www.youtube-nocookie.com/embed/CLKwosydXsc?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In today's video we'll explore how to create :ref:`custom metrics <metrics-custom-metrics>`
with Blackfire, specially tailored to your application's unique needs.

Blackfire already provides over 600 built-in metrics. Sometime we need metrics
specific to our own code and logic. That's when custom metrics become very useful.

Custom metrics are also stored in our ``.blackfire.yaml`` file. Suppose you want
to measure the time spent on a particular method like rendering your main
controller. You can create a custom metric for that.

This metric measures every calls to the ``MainController::render`` method. As
for any other metric, you will see its cardinality in the
:doc:`Deterministic Profile UI </academy/profiling/understanding-callgraphs>`,
which means how many times that metric has been identified, as well as its
contribution to all available dimensions.

In some cases you won't be interested in all that information. You can define
which contribution you are interested in with the ``contrib`` key. Are you
interested in the count only? The cost only? The cost being the contribution to
all dimensions. Or even both of them, which is the default option.

Timeline Metrics
~~~~~~~~~~~~~~~~

Timeline metrics are those metrics listed at the top of the metric list and
associated with a colored background to be better identified. You can have your
custom metrics in that list by adding the ``timeline: true`` option.

Using Markers
~~~~~~~~~~~~~

Another option to improve the visibility of a custom metric is to have a marker
displayed every time the metric is detected. This is possible by adding the
``marker`` option with the description of that marker. This is a great
debugging tool.

Our custom metrics can be precise and super flexible at the same time. Not only
can we define one or more callees, which are the functions being called, but you
can define callers as well.

You can target when a specific function is being called by another specific
method. This allows you laser-focused performance insights.

Using Regular Expressions
~~~~~~~~~~~~~~~~~~~~~~~~~

You can go even beyond this by using regular expressions. You could even target
classes implementing a specific interface. This is truly a powerful feature and
the Jedi way of mastering Blackfire. Check the :doc:`documentation </testing-cookbooks/metrics>`
under **Tests** > :doc:`Metrics </testing-cookbooks/metrics>` to discover all
the options available.

In that documentation, you will learn, for instance, about argument capturing,
giving you the possibility to group function calls by specific arguments. This
is a great way to bring more clarity to your profile information.

Nesting Metrics
~~~~~~~~~~~~~~~

Finally, if your customer metrics start growing, a good practice is to organize
them with layers. What about grouping the custom metrics for your databases
operation, user management, or billing?

The ``layer`` key is your option to create, well, layers. Note that those layers
can be nested as well. The ``billing`` layer can be split into
``billing.invoice``, ``billing.refund``, themselves could also hold more nested
layers.

Using custom metrics allows you to measure exactly what matters to your
application. They make your performance test more reliable and help you enforce
higher standards.

Your next step is to create your first custom metric. Then we will see how to
start :doc:`automating performance testing <scenarios>` to secure your critical
customer journeys.
