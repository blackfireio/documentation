Browser Monitoring & Analytics Usage
====================================

Detailed information on the Browser Monitoring & Analytics traces consumption
can be found under the Organization Usage menu:

.. image:: ../images/organization-browser-usage-menu.png
    :width: 400px
    :align: center

This view shows the number of browser traces consumed in environments you
have access to.

The traces used in the organization's other environments are gathered within
the "Other environments" entry.

.. image:: ../images/front-end/browser-usage.png

Traffic Spike Prevention
------------------------

Blackfire Browser Monitoring and Analytics's traffic spike prevention system
protects your monthly browser quota from sudden traffic surges.

It continuously tracks your browser traces collection rate. At any time, an
ingestion rate exceeding 15 times your monthly quota allowance is identified as
an abnormal traffic spike.

Blackfire monitoring and analytics are then automatically paused for 15 minutes.
Subsequently, those features resume automatically, ensuring you continue to
receive insights without significant disruption.
