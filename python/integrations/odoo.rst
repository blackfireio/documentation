Odoo [language: Python]
=========================

.. _python-odoo:

`Odoo <https://www.odoo.com>`_ is a suite of business management software written in Python.

We provide an integration allowing the performance measurement of individual HTTP requests.

Requirements
------------

- Odoo 13 and higher


Automatic Instrumentation
-------------------------

The recommended way to use Blackfire with Odoo is to use the
:ref:`blackfire-python command <blackfire-python>`, as it configures the needed
bits for you.

Run your webserver with ``blackfire-python`` command:

.. code-block:: bash

    blackfire-python odoo-bin


Manual Installation
-------------------

If you prefer configuring Odoo manually, add the following call within your code:

.. code-block:: python

    import blackfire
    blackfire.patch_all()

This call should be made **as early as possible** in the lifecycle of an application,
**ideally before any other** ``import`` **statements**.

Then, restart your server.


Profiling HTTP Requests
-----------------------

You can use the ``blackfire curl`` command to profile specific requests:

.. code-block:: bash

    blackfire curl http://localhost:8069/web

You can also use one of our browser extensions for :doc:`Firefox
</integrations/browsers/firefox>` or :doc:`Chrome
</integrations/browsers/chrome>`.

Read more about :doc:`profiling web applications with a browser
</profiling-cookbooks/profiling-http-via-browser>`, or :doc:`profiling with the CLI
</profiling-cookbooks/profiling-http-via-cli>`.
