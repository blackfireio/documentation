.. _blackfire-python:

blackfire-python [language: Python]
===================================

The ``blackfire-python`` command is being installed along with the Blackfire
``pip`` package. **It can be used to enable the Probe automatically when a profile
is requested**, without modifying your code.

.. note::

    No profile is triggered automatically with this command.

Supported Frameworks
--------------------

``blackfire-python`` currently supports:

* Django

* Flask

* Odoo

Usage with HTTP Servers
-----------------------

To ensure that your application listens to profile requests, you need
to run your webserver through ``blackfire-python`` command.

Example with Django development server:

.. code-block:: bash

    blackfire-python python manage.py runserver

Example with Django using ``gunicorn``:

.. code-block:: bash

    blackfire-python gunicorn myapp.wsgi

Usage with CLI Commands
-----------------------

To be able to run CLI commands and profile them, you need to use
``blackfire-python run`` command:

.. code-block:: bash

    blackfire-python run python my_command.py
