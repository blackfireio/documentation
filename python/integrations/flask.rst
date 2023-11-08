Flask [language: Python]
========================

Our Flask integration lets you instrument individual HTTP requests. Please note 
that Blackfire supports Flask 0.12 and higher.

:doc:`Install Blackfire for Python </install/python>`.

Automatic Instrumentation
-------------------------

The recommended way to use Blackfire with Flask is to use the
:ref:`blackfire-python command <blackfire-python>`, as it configures the needed
bits for you.

Run your webserver with ``blackfire-python`` command:

.. code-block:: bash

    export FLASK_APP=hello.py
    blackfire-python flask run

Or with ``gunicorn``:

.. code-block:: bash

    blackfire-python gunicorn myproject:app

Manual Installation
-------------------

If you prefer configuring Flask manually, you can add the following call
manually within your code:

.. code-block:: python

    import blackfire
    blackfire.patch_all()

This call should be made **as early as possible** in the lifecycle of an application,
**ideally before any other** ``import`` **statements**.

Then, restart your server.

.. caution::

    We used to provide a Flask middleware along with the Blackfire Python SDK,
    ``blackfire.middleware.FlaskMiddleware``.

    This middleware is now deprecated in favor of the ``blackfire-python`` or the
    ``blackfire.patch_all()`` call.
    Using the middleware will trigger a deprecation warning.

Profiling HTTP Requests
-----------------------

You can use the ``blackfire curl`` command to profile specific requests:

.. code-block:: bash

    blackfire curl http://localhost:5000/

You can also use one of our browser extensions for :doc:`Firefox
</integrations/browsers/firefox>` or :doc:`Chrome
</integrations/browsers/chrome>`.

Read more about :doc:`profiling web applications with a browser
</profiling-cookbooks/profiling-http-via-browser>`, or :doc:`profiling with the CLI
</profiling-cookbooks/profiling-http-via-cli>`.
