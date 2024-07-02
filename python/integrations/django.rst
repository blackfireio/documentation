Django [language: Python]
=========================

.. _python-django:

Our Django integration lets you instrument individual HTTP requests. Please note
that Blackfire supports Django 1.11 and higher.

:doc:`Install Blackfire for Python </install/python>`.

.. caution::

    Blackfire Django integration has compatibility issues with the
    Django debug toolbar. You may consider disabling the Django debug
    middleware when using Blackfire.

Automatic Instrumentation
-------------------------

The recommended way to use Blackfire with Django is to use the
:ref:`blackfire-python command <blackfire-python>`, as it configures the needed
bits for you.

Run your webserver with ``blackfire-python`` command:

.. code-block:: bash

    blackfire-python python manage.py runserver

Or with ``gunicorn``:

.. code-block:: bash

    blackfire-python gunicorn myapp.wsgi

Manual Installation
-------------------

If you prefer configuring Django manually, you can add the following call
manually within your code:

.. code-block:: python

    import blackfire
    blackfire.patch_all()

This call should be made **as early as possible** in the lifecycle of an application,
**ideally before any other** ``import`` **statements**.

Then, restart your server.

.. caution::

    We used to provide a Django middleware along with the Blackfire Python SDK,
    ``blackfire.middleware.DjangoMiddleware``.

    This middleware is now deprecated in favor of the ``blackfire-python`` or the
    ``blackfire.patch_all()`` call.
    Using the middleware will trigger a deprecation warning.

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
