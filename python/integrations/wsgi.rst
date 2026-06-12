WSGI Middleware [language: Python]
==================================

WSGI (Web Server Gateway Interface) is a specification that defines the protocol
between web servers and Python web applications.

The Blackfire Python SDK contains a middleware easing the integration with WSGI
web applications.

The integrations we provide for :doc:`Django <django>`, :doc:`Flask <flask>`,
:doc:`Odoo <odoo>` are extending the ``BlackfireWSGIMiddleware``. They could
`serve as examples <https://github.com/blackfireio/python-sdk/tree/master/hooks>`_
helping the creation of a new middleware.

Integrations with other frameworks could benefit the Blackfire community. Please
consider :route:`contributing your code <contact-us>`.

Installation
------------

The Blackfire Python SDK is available :doc:`with the Blackfire Python Package
</up-and-running/installation>`.

Configuration
-------------

Create a class extending the ``BlackfireWSGIMiddleware``.

The ``FRAMEWORK`` variable must be set; it should describe the instrumented
application.

.. code-block:: python
    :emphasize-lines: 5

    from blackfire.hooks.wsgi import BlackfireWSGIMiddleware

    class BlackfireFooBarMiddleware(BlackfireWSGIMiddleware):

        FRAMEWORK = 'Foo-Bar'

        ...

Monitoring [level: Production]
------------------------------

A ``get_view_name`` method must be defined to have the requests of your WSGI-based
application be instrumented by :doc:`Blackfire Monitoring</monitoring-cookbooks/index>`.

This function is required only for the monitoring of your application. Its
definition can be omitted if you are not considering it.

The ``get_view_name`` method retrieves the view name executing or handling the
HTTP request. Blackfire Monitoring relies on this information to :doc:`group
requests in the monitoring dashboard</monitoring-cookbooks/naming-transactions>`.

If it returns ``None``, the viewname will be grouped with other :ref:`Unnamed
Transactions<monitoring_unnamed_transactions>`

The function receives 1 parameter:

* ``environ`` is a `dictionary <https://peps.python.org/pep-0333/#environ-variables>`_
  that contains the HTTP request headers and other metadata.

The function should return a ``string`` or ``None``.

.. code-block:: python
    :emphasize-lines: 7

    from blackfire.hooks.wsgi import BlackfireWSGIMiddleware

    class BlackfireFooBarMiddleware(BlackfireWSGIMiddleware):

        FRAMEWORK = 'Foo-Bar'

        def get_view_name(self, environ):
            # implementation ...
