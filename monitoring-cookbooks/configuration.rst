Configuring Blackfire Monitoring
================================

Blackfire Profiler and Blackfire Monitoring use :ref:`the same software stack
<blackfire-stack>`. See how to :doc:`get started </up-and-running/index>`.

.. note::

    Blackfire Monitoring currently supports PHP 7 and higher on Linux, BSD,
    macOS and Windows (via Windows Subsystem for Linux).

    Python supports Python 2.7 and higher.

Activating Monitoring on an Environment
---------------------------------------

To activate Blackfire Monitoring on an :doc:`environment </reference-guide/environments>`,
you need to be manager of that environment or an :doc:`organization admin
</up-and-running/access-management/environment-levels>`.

To activate Blackfire Monitoring on the relevant :doc:`environment </reference-guide/environments>`:

#. Go to your organization menu and click :ref:`Organization Monitoring Usage <monitoring-activation>`.

#. Click **Enable**.

.. note::

    Blackfire Monitoring is enabled by default since PHP Probe version ``1.61.0``
    and Python Probe version ``1.18.0``. Check the
    :doc:`PHP probe configuration </php/configuration>` and the
    :doc:`Python probe configuration </php/configuration>`  if you want to
    explicitly disable it.

Configuring Monitoring Settings
-------------------------------

.. _monitoring_sample_rate:

Sample Rate
~~~~~~~~~~~

The Sample Rate represents the percentage of your PHP requests which you would
like Blackfire to monitor.

Each request which is monitored generates a "Trace". This tracing level captures
general performance metrics, such as overall response time and memory usage,
and generates **close-to-no overhead**.

We highly recommend you to monitor at least 80% of your requests, but as Blackfire
Monitoring pricing is based on a quota of Traces, you can balance:

- changing your Trace Quota and control the subscription costs;

- changing your Sample Rate and control the monitoring granularity.

.. _monitoring_extended_sample_rate:

Extended Sample Rate
~~~~~~~~~~~~~~~~~~~~

The Extended Sample Rate represents the percentage of Traces for which Blackfire
will collect more in-depth metrics.

Especially, such Extended Traces will include Spans.

A Span is the representation of a function call over time, just like in a
:doc:`profile timeline </profiling-cookbooks/understanding-timelines>`.

Collecting Spans may generate additional overhead on Extended Traces.

With the Extended Sample Rate, you can balance:

- the number of end-user requests which may be impacted by the overhead;

- the possibility for you to collect in-depth performance metrics with
  "real-world" context.

.. _monitoring_span_treshold:

.. note::

    Blackfire Monitoring natively supports all PHP applications. For some
    frameworks, including Symfony, Drupal, Prestashop 1.7+, and Ibexa DXP,
    Blackfire Monitoring already collects the most significant Spans, while
    avoiding to add more than 15% overhead (maximum currently measured).
