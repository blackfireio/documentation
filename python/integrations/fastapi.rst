FastAPI [language: Python]
=========================

.. _python-fastapi:

Our FastAPI integration lets you instrument individual HTTP requests. Please note
that Blackfire supports FastAPI `0.51.0` and higher.

:doc:`Install Blackfire for Python </install/python>`.

Automatic Instrumentation
-------------------------

The recommended way to use Blackfire with FastAPI is to use the
:ref:`blackfire-python command <blackfire-python>`, as it configures the needed
bits for you.

Run your webserver with ``blackfire-python`` command:

.. code-block:: bash

    blackfire-python uvicorn main:app

Or with ``hypercorn``:

.. code-block:: bash

    blackfire-python hypercorn main:app

Manual Installation
-------------------

If you prefer configuring FastAPI manually, you can add the following call
manually within your code:

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

    blackfire curl http://localhost:8000/polls/1/results

You can also use one of our browser extensions for :doc:`Firefox
</integrations/browsers/firefox>` or :doc:`Chrome
</integrations/browsers/chrome>`.

Read more about :doc:`profiling web applications with a browser
</profiling-cookbooks/profiling-http-via-browser>`, or :doc:`profiling with the CLI
</profiling-cookbooks/profiling-http-via-cli>`.
