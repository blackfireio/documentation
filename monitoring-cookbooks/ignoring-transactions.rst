.. _monitoring_ignoring_transactions:

Ignoring Transactions
=====================

In some cases, you might not want Blackfire Monitoring to
:doc:`instrument transactions </monitoring-cookbooks/naming-transactions>`.

You can programmatically ignore them using the ``ignoreTransaction()`` method:

**PHP Application**

.. code-block:: php

    // As of Blackfire PHP Probe 1.57.0
    \BlackfireProbe::ignoreTransaction();

**Python Application**

.. code-block:: python

    from blackfire import apm

    # As of Blackfire Python Probe 1.6.1
    apm.ignore_transaction();
