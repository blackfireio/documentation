Naming Transactions
===================

.. include-twig:: `youtube-iframe`
    :title: Naming Transactions
    :src: https://www.youtube-nocookie.com/embed/3LA7BqROq_Q?rel=0&showinfo=0&modestbranding=1&autoplay=0
    :width: 700px
    :height: 394px

Video Transcript
----------------

In this video, we'll explore how to :doc:`name transactions </monitoring-cookbooks/naming-transactions>`
in your applications so that you can get better insights from Blackfire Monitoring.

In Blackfire monitoring, a :term:`transaction <Transaction>` is a group of
server-side requests traced by Blackfire and associated with a specific name.
This name corresponds to whatever logical unit fits into your framework or
code best: a controller action, a function call, or even a view.

For some frameworks, like :doc:`Symfony </php/integrations/symfony/index>`,
:doc:`Laravel </php/integrations/laravel/index>`,
:doc:`Magento </php/integrations/magento>` or
:doc:`Django </python/integrations/django>`, Blackfire Monitoring
automatically detects transaction names. However, they appear under
:ref:`Unnamed transactions <monitoring_unnamed_transactions>` when we can't
automatically name them.

:ref:`Unnamed transactions <monitoring_unnamed_transactions>` is basically a
catch all bucket for any request that Blackfire can't name by default. While you
can manually name them in the UI, the most powerful and flexible method is to
name these transactions programmatically.

Let's see how to :ref:`name transactions in code <monitoring_naming_transactions_programmatically>`.
First, The ``setTransactionName`` method that comes with Blackfire Probe for PHP
and Python is designed to assign a name to a transaction programmatically.

Same goes with ``startTransaction``, the method used to monitor CLI commands and
services. Passing a parameter to it defines the transaction name for the transaction
linked to the code executed between ``startTransaction`` and ``stopTransaction``.

Programmatically naming transaction is favored, as it enables the
**profile next request** and **automatic profiling** features.

Alternatively, and if you prefer a no code approach, you can configure custom
transaction names from the unnamed transaction screen or the monitoring settings
in Blackfire. You can match incoming requests and assign them to a name, using
either a glob pattern or a regular expression.

But keep in mind that manually named transaction from the UI cannot be profiled
automatically or targeted by the **profile next request** CTA. Only programmatic
naming allows for these features.
