Mark Events in the Monitoring Timeline
======================================

You may want to visualize specific events in your Monitoring timeline to check
the impact of an action, like a deployment.

.. image:: ../images/monitoring/monitoring-events.png

It is possible to mark events in the Monitoring timeline using the following curl
command:

.. include-twig:: `apm_event_credentials`

.. note::

    The ``name`` parameter can be up to 64 characters long.
