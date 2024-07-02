Health Report
=============

The Health Report compiles key metrics and actionable insights from
:doc:`Blackfire Monitoring </monitoring-cookbooks/index>` and :doc:`Blackfire Builds
</builds-cookbooks/index>`.

To benefit from all of the Health Report features, we strongly recommend to
activate at least, on a given environment:

- :doc:`Periodic Builds </builds-cookbooks/builds-periodic>`;
- :doc:`Monitoring </monitoring-cookbooks/configuration>`.

.. note::

    The Health Report generates an overview of your application's performance
    over 7 days. It compares it with the previous 7 days period.

    Therefore, to generate a thorough Health Report, Blackfire Builds and
    Monitoring should run on a given environment for a period of at least 14
    days.

    Some advanced metrics are compiled over 6 weeks of data collection.

Health Report Email
-------------------

A summary of the Health Report is sent every Monday, from 9.00am according to
the time zone configured in your environment settings.

You can change your subscription settings for the Health Report separately from
other email notifications via `your personal settings <https://blackfire.io/my/settings/notifications>`_.
