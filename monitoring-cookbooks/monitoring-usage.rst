Monitoring Usage
=================

Detailed information on the Monitoring traces consumption can be found under the
Organization Usage menu:

.. image:: ../images/organization-usage-menu.png
    :width: 400px
    :align: center

.. _monitoring-activation:

Monitoring Activation
----------------------

This view lists the environments you has access to.

You can manage the settings of the environments you administrate.

.. image:: ../images/monitoring/monitoring-activation.png

Monitoring Usage
-----------------

This view shows the number of monitoring traces consumed in environments you
have access to.

The traces used in the organization's other environments are gathered within
the "Other environments" entry.

.. image:: ../images/monitoring/monitoring-usage.png

Traffic Spike Prevention
------------------------

Blackfire Monitoring's traffic spike prevention system protects your monthly
monitoring quota from sudden traffic surges.

It continuously tracks your monitoring traces collection rate. At any time, an
ingestion rate exceeding 15 times your monthly quota allowance is identified as
an abnormal traffic spike.

Blackfire monitoring is then automatically paused for 15 minutes. Subsequently,
monitoring resumes automatically, ensuring you continue to receive insights
without significant disruption.
