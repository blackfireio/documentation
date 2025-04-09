Extend your Performance Tests with Custom Metrics
=================================================

.. include-twig:: `youtube-iframe`
    :title: Writing custom metrics
    :src: https://www.youtube-nocookie.com/embed/CLKwosydXsc?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

In addition to the metrics it provides, Blackfire allows you to define custom
metrics based on your application's logic.

These customized metrics could be the most powerful ones you could use in your
performance tests.

Custom metrics are defined in your ``.blackfire.yaml`` file:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            # Short label for humans
            label: 'Markdown to HTML'

            # Longer description for humans
            description: 'Metric for Markdown to HTML conversion'

            matching_calls:
                php:
                    -
                        callee: "=App\\Utils\\Markdown::toHtml"

As for all metrics, custom metrics can be used when defining assertions.

Custom metrics target the execution of specific functions. You can list multiple
functions (``callee``) and even define a ``caller`` to target a specific sequence
of calls:

.. code-block:: yaml

    metrics:
        markdown_to_html:
            matching_calls:
                php:
                    -
                        caller: "=App\\Twig\\AppExtension::markdownToHtml"
                        callee: "=App\\Utils\\Markdown::toHtml"
                    -
                        callee: "=App\\Utils\\AlternativeMarkdown::toHtml"

Callers and callee can be defined as regular expressions. You can also target all
the classes implementing a class or an interface.

.. note::

    :doc:`Explore the possibilities </testing-cookbooks/metrics>`, such as
    capturing arguments and adding markers to your timelines
