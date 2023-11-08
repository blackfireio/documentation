Pager Duty [level: Production]
==============================

PagerDuty + Blackfire Integration Benefits
------------------------------------------

- Notify on-call responders based on alerts sent from Blackfire Monitoring;

- Create high and low urgency incidents based on the notification type (alarm / warning).

How it Works
------------

The `PagerDuty <https://www.pagerduty.com/>`_ notification channel creates
incidents on your PagerDuty **Service** whenever a :doc:`Monitoring alert is
triggered </monitoring-cookbooks/alerting>`.

Support
-------

If you need help with this integration, please `contact Blackfire support
<https://support.blackfire.platform.sh>`_.

Integration Walkthrough
-----------------------

**In PagerDuty**
~~~~~~~~~~~~~~~~

1. From the **Configuration** menu, select **Services**;

2. There are two ways to add an integration to a service:

   - **If you are adding your integration to an existing service**:
     Click the **name** of the service you want to add the integration to.
     Then, select the **Integrations** tab and click the **New Integration** button;

   - **If you are creating a new service for your integration**: Please read
     PagerDuty documentation in section `Configuring Services and Integrations
     <https://support.pagerduty.com/docs/services-and-integrations#section-configuring-services-and-integrations>`_
     and follow the steps outlined in the `Create a New Service section
     <https://support.pagerduty.com/docs/services-and-integrations#section-create-a-new-service>`_,
     selecting **Blackfire.io** as the Integration Type in step 4. Continue with
     the :ref:`In Blackfire section <pagerduty_in_blackfire>` (below) once you
     have finished these steps;

3. Enter an **Integration Name** in the format ``<monitoring-tool>-<service-name>``
   (e.g. ``blackfire-Shopping-Cart``) and select **Blackfire.io** from the
   Integration Type menu;

4. Click the **Add Integration** button to save your new integration.
   You will be redirected to the Integrations tab for your service;

5. An **Integration Key** will be generated on this screen. Keep this key saved
   in a safe place, as it will be used when you configure the integration with
   **Blackfire** in the next section;

.. _pagerduty_in_blackfire:

**In Blackfire**
~~~~~~~~~~~~~~~~

1. From one of your :doc:`Blackfire Environments </reference-guide/environments>`,
   go to **Settings**, and then click on **Notification Channels**;

2. Click on the **Add Notification Channel** button, and then click on
   **Add PagerDuty**;

3. Give the Notification Channel a name, and paste your PagerDuty **Integration Key**
   in the corresponding field;

4. Click on the **Save** button.

You are now ready to use the PagerDuty as a notification channel for Blackfire
Monitoring!
